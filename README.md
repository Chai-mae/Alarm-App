# Alarm-App

![111](https://user-images.githubusercontent.com/93831197/152684997-86eae776-7735-4c29-82fa-180c30ce009a.jpeg)
 
 
 In our final project we have chosen to work on an Alarm application. In fact this application has been a good opportunity for us to practice the skills we have learned in writing multi-platform GUI applications using the Qt library Course. 
 
**<h2>Application description</h2>**

 
Our application is implemented using the MVC model :

* QStandardItemModel as a model :QStandardItemModel can be used as a repository for standard Qt data types. It is one of the Model/View Classes and is part of Qt's model/view framework. QStandardItemModel provides a classic item-based approach to working with the model. The items in a QStandardItemModel are provided by QStandardItem.
* QListView as a view : The QListView class implements a list/tree view. It can display and control a hierarchy of multi-column items, and provides the ability to add new items at any time. Among others the user may select one or many items and sort the list in increasing or decreasing order by any column.

Our application has the following features :

* Alarm

![UNO](https://user-images.githubusercontent.com/93831197/152685657-942fc2bf-2be0-4f3c-8874-daca06177a95.jpeg)

* Chronometer

![DOS](https://user-images.githubusercontent.com/93831197/152685669-dfba9060-e5c1-4e2a-8f51-940cbe02fc47.jpeg)

* Timer

![TRES](https://user-images.githubusercontent.com/93831197/152685673-f176ebd0-5665-4f8b-bd0b-d5f8dbddca35.jpeg)

* Analog ClocK

![QA](https://user-images.githubusercontent.com/93831197/152685679-f514240f-13c0-4046-a7e6-9d984afe3c0c.jpeg)

The main window is the Alarm window which contains five QPushButtons  one for deleting an existing alarm, one for adding a new alarm, one for the timer, the fourth one for the chronometer and the last one for the analog clock.

It contains also a QListView in which the alarmsare displayed. At the top of the main window, there is a QLCDNumber that displays the current time.

**<h2>Alarm Functionality:</h2>**

This is the main functionality of our application. To set a new alarm we need to click on the plus button at the top right of the main window. The following QDialog window appears :

![HAY](https://user-images.githubusercontent.com/93831197/152686107-f3392dcf-2fb0-4a6e-9046-641914b0c7dd.jpeg)


