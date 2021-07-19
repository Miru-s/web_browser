## Mirnalin's Browser

# Web-browser Code 
IDE used- Pycharm


from PyQt5.QtWidgets import *
import sys
from PyQt5.QtWebEngineWidgets import *
from PyQt5.QtCore import *



class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.browser = QWebEngineView()
        self.browser.setUrl(QUrl('https://www.google.co.in/'))
        self.setCentralWidget(self.browser)
        self.showMaximized()

        #navbar
        navbar = QToolBar()
        self.addToolBar(navbar)

        back_btn = QAction('Back', self)
        back_btn.triggered.connect(self.browser.back)
        navbar.addAction(back_btn)

        forward_btn = QAction('Forward',self)
        forward_btn.triggered.connect(self.browser.forward)
        navbar.addAction(forward_btn)

        reload_btn= QAction('Reload',self)
        reload_btn.triggered.connect(self.browser.reload)
        navbar.addAction(reload_btn)

        home_btn= QAction('Home',self)
        home_btn.triggered.connect(self.navigate_home)
        navbar.addAction(home_btn)

        self.url_bar = QLineEdit()
        self.url_bar.returnPressed.connect(self.navigate_to_url)
        navbar.addWidget(self.url_bar)

        self.browser.urlChanged.connect(self.update_url)


    def navigate_home(self):
        self.browser.setUrl(QUrl('https://www.google.com/'))

    def navigate_to_url(self):
        url = self.url_bar.text()
        self.browser.setUrl(QUrl(url))

    def update_url(self, url):
        self.url_bar.setText(url.toString())




app = QApplication(sys.argv)
QApplication.setApplicationName('Mirnalin Browser')
window = MainWindow()
app.exec()



Explanation
GUI Implementation steps :
1. Create a main window
2. Create a QTabWidget for tabbing, set it as central widget, make them documented and closable, below is how the tabs will look like
3. Create a status bar to show the status tips
4. Create a toolbar and add a navigation button and the line edit to show the URL.
 
 
Back-End Implementation Steps :
1. Add action to the QTabWidget object when double-clicked is pressed
2. Inside the double click action check if the double click is on no tab then call the open tab method
3. Inside the open tab, method create a QUrl object and the QWebEngineView object and set QUrl to it and get the index of the tab
4. Add update url action to QWebEngineView object when url is changed.
5. Inside the update, url action check if action is called by the opened tab then change the url of url bar and change cursor position
6. Add another update title action to the QWebEngineView object when loading is finished
7. Inside the update title method update the title of the window as the page title if the action is called by the open tab only
8. Add action to the tabs when the tab is changed
9. Inside the tab changed action get the url update the url inline edit and the title
10. Add actions to the navigation buttons using the built-in functions of the QWebEngineView object for reloading, back, stop and forward buttons
11. Add action to the home button and inside the action change the url to google.com
12. Add action to the line edit when the return key is pressed
13. Inside the line, edit action get the text and convert this text to the QUrl object and set the scheme if it is null and set this url to the current tab.
 
 
 
PyQt5 is a cross-platform GUI toolkit, a set of python bindings for Qt v5. One can develop an interactive desktop application with so much ease because of the tools and simplicity provided by this library. 
 
The python sys module provides functions and variables which are used to manipulate different parts of the Python Runtime Environment. It lets us access system-specific parameters and functions.
 
 
 
 


https://user-images.githubusercontent.com/78691192/126109033-f69d684c-46ff-49be-8487-dda2aeb144f2.mp4

