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

In this dialog we set the description and the time of the alarms as well as we choose the ring tone that we want to be played.
Once the OK button is clicked the alarm is fixed, it is added to our model and displayed in our view. This done through the following getters defined in the AddAlarmDialog class: 
 ```javascript
QStringAddAlarmDialog::getDesc(){
returnui->lineEdit->text();
}
QStringAddAlarmDialog::getTimeSting(){
returnui->timeEdit->text();
}
QStringAddAlarmDialog::getRingTone(){
returnui->comboBox->currentText();
}
QTimeAddAlarmDialog::getTime(){
returnui->timeEdit->time();
}
```
Here is the code of the add slot connected the plus button :

```javascript
voidWidget::on_pushButton_2_clicked()
{
AddAlarmDialogdialog;
autoreply=dialog.exec();
if(reply==AddAlarmDialog::Accepted)
{
item=newQStandardItem();

item->setText(dialog.getTimeSting()+" "+dialog.getDesc()+" "+dialog.getRingTone());

item->setCheckable(true);
item->setCheckState(Qt::Checked);

model->appendRow(item);

ui->listView->setModel(model);
}
}
```
In this slot we set our QStandardItem to Qt::checked.

Once the time set in the alarm is equal to the current time,the alarm starts to ring and a QDialog window shows up asking whether the user wants to stop the alarm or to repeat it after one minute. 

![Capture d’écran 2022-02-06 182456](https://user-images.githubusercontent.com/93831197/152693043-7bc107ce-f5ff-477c-8aa3-25714ac5aba5.png)

Here is the code of this functionality :
```javascript
voidWidget::showTime(){

QTimet=QTime::currentTime();
QStringtext=t.toString("hh:mm");
ui->lcdNumber->display(text);


RingDialogd;
for(inti=0;i<model->rowCount();i++){
QStrings=model->item(i)->text();
QStringListlist=s.split(" ");

if(model->item(i)->checkState()&&text==list[0]){
timer->start(60000);

if(list[2]=="RingTone1"){
ring->setMedia(QUrl("qrc:/ring1.mp3"));
ring->play();

}
elseif(list[2]=="RingTone2"){
ring->setMedia(QUrl("qrc:/ring2.mp3"));
ring->play();
}
else{
ring->setMedia(QUrl("qrc:/ring3.mp3"));
ring->play();
}
autoreply=d.exec();
if(reply==RingDialog::Accepted)
{

ring->stop();

}
elseif(reply==RingDialog::Rejected){
ring->stop();
QStringListlist2=list[0].split(":");
inta=list2[1].toInt()+1;
QStringb=QString::number(a);
l.append(list2[0]+":"+b+" "+list[1]+" "+list[2]);


}

}
}
for(inti=0;i<l.size();i++){

QStringListlist3=l[i].split(" ");
qDebug()<<list3[0];
if(text==list3[0]){
std::cout<<"test";
if(list3[2]=="RingTone1"){
ring->setMedia(QUrl("qrc:/ring1.mp3"));
ring->play();

}
elseif(list3[2]=="RingTone2"){
ring->setMedia(QUrl("qrc:/ring2.mp3"));
ring->play();
}
else{
ring->setMedia(QUrl("qrc:/ring3.mp3"));
ring->play();
}
autoreply=d.exec();
if(reply==RingDialog::Accepted)
{

ring->stop();
l.removeAt(i);
}
elseif(reply==RingDialog::Rejected){
ring->stop();
QStringListlist2=list3[0].split(":");
inta=list2[1].toInt()+1;
QStringb=QString::number(a);
l.removeAt(i);
l.append(list2[0]+":"+b+" "+list3[1]+" "+list3[2]);


}
}

}
}

```

In this function, we declared a QTime object that has the current time as a value. This time is displayed in the QLCDNumber widget. After that, we loop through our model searching for the the alarm that is checked and that needs to ring. The sound in played using the QMediaPlayer library which allows the playing of a media source.
If we want to delete an existing alarm we just need to click on the delete button. Here is the code of this functionality :
```javascript
voidWidget::on_pushButton_clicked()
{
model->removeRow(ui->listView->currentIndex().row());
ui->listView->setModel(model);

}

```

In order to keep our previous alarms, we have stored them in a file so that once the application is opened we can find them. To do this we re-implemented the closeEvent() event .This event handler is called with the given event when Qt receives a window close request for a top-level widget from the window system.
Here is the code :
```javascript
voidWidget::closeEvent(QCloseEvent*e){
QFilefile("currentFile.txt");
if(file.open(QIODevice::ReadWrite|QIODevice::Text)){
QTextStreamout(&file);
for(inti=0;i<model->rowCount();i++){
if(model->item(i)->text().at(0)==" "){

}elseif(model->item(i)->checkState()){
out<<"1"<<model->item(i)->text()<<Qt::endl;
}else{
out<<"0"<<model->item(i)->text()<<Qt::endl;
}
}
file.close();
}
}

```
