## Overview

The goal of the homework is to create an application to manage you tasks. It should have all the features of main application such as menues, actions and toolbar. The application must store an archive of all the pending and finished tasks.

![image](https://user-images.githubusercontent.com/86810485/150678134-616360ce-ce43-46d2-a71e-680b7420e42a.png)

## Use Cases

Here is a list of cases that the user could perform with our app:

  1. A user should be able to close the application of course.
  
  2. A Todo application cannot be useful, unless it offers the possibility of creating new tasks.
        *The essential components of a task will be defined later
        
  3. The View of the main widget should be split in three areas:

         1-The first (en persistent) area shows the list of today tasks.
         
         2- The second one is reserved for pending task (tasks for the future).
         
         3- Finally, the third one shows the set of finished tasks.
         
  4.Each category must be shown with a custom icon.

  5.The user could either the pending and finished views.hide/show

  6.Finally, the tasks entered to your application must remains in the app in future use.

       Meaning, If I create a task and I close the application, next time I opened the application, I should find my tasks and not start from scratch.
       
## Defining a Task   
 A is defined by the following attributes:Task

  *A : stating the text and goal for the task like (Buying the milk).description

  *A boolean indicating if the task is Finished or due.finished
  
  *A category to show the class of the task which is reduced to the following values:Tag

     .Work
     .Life
     .Other
     
*Finally, a task should have a which stores the Date planned for the date.DueDate


When the user create a new task, the application must pop up a dialog for the user to get those values. Here is an example ( not mandatory, I prefer you create your own) example:     
       
 ![image](https://user-images.githubusercontent.com/86810485/150679201-69a186e5-8102-4823-a15e-662bd574eef2.png)


  ## remtache.h

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">ifndef</span><span style="color:#004a43; "> REMTACHE_H</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">define</span><span style="color:#004a43; "> REMTACHE_H</span>

<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QDialog</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">ctime</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QString</span><span style="color:#800000; ">&gt;</span>
<span style="color:#800000; font-weight:bold; ">namespace</span> Ui <span style="color:#800080; ">{</span>
<span style="color:#800000; font-weight:bold; ">class</span> remTache<span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">class</span> remTache <span style="color:#800080; ">:</span> <span style="color:#800000; font-weight:bold; ">public</span> <span style="color:#603000; ">QDialog</span>
<span style="color:#800080; ">{</span>
    <span style="color:#004a43; ">Q_OBJECT</span>

<span style="color:#800000; font-weight:bold; ">public</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">explicit</span> remTache<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#808030; ">~</span>remTache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QString</span> getDescription<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">;</span>      <span style="color:#696969; ">//un getter pour recupperer la description de la tache</span>
    <span style="color:#603000; ">QDate</span> getDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">bool</span> isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">;</span>
<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
    Ui<span style="color:#800080; ">::</span>remTache <span style="color:#808030; ">*</span>ui<span style="color:#800080; ">;</span>
<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">void</span> updateDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>

<span style="color:#004a43; ">#</span><span style="color:#004a43; ">endif</span><span style="color:#004a43; "> </span><span style="color:#696969; ">// REMTACHE_H</span>
</pre>

## remtache.cpp


<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">remtache.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">ui_remtache.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QDate</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QDateTimeEdit</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QString</span><span style="color:#800000; ">&gt;</span>

remTache<span style="color:#800080; ">::</span>remTache<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent<span style="color:#808030; ">)</span> <span style="color:#800080; ">:</span>
    <span style="color:#603000; ">QDialog</span><span style="color:#808030; ">(</span>parent<span style="color:#808030; ">)</span><span style="color:#808030; ">,</span>
    ui<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> Ui<span style="color:#800080; ">::</span>remTache<span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setupUi<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    updateDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

remTache<span style="color:#800080; ">::</span><span style="color:#808030; ">~</span>remTache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> ui<span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> remTache<span style="color:#800080; ">::</span>updateDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    <span style="color:#603000; ">QDate</span> D<span style="color:#808030; ">=</span><span style="color:#603000; ">QDate</span><span style="color:#800080; ">::</span>currentDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>dateEdit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setMinimumDate<span style="color:#808030; ">(</span>D<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>dateEdit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setDate<span style="color:#808030; ">(</span>D<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>

<span style="color:#603000; ">QString</span> remTache<span style="color:#800080; ">::</span>getDescription<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">return</span> ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>lineEdit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>text<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Due : </span><span style="color:#800000; ">"</span><span style="color:#808030; ">+</span> ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>dateEdit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>text<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">+</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">Tag : </span><span style="color:#800000; ">"</span><span style="color:#808030; ">+</span> ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>comboBox<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>currentText<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">+</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#603000; ">QDate</span> remTache<span style="color:#800080; ">::</span>getDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">return</span> ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>dateEdit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>date<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">bool</span> remTache<span style="color:#800080; ">::</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800000; font-weight:bold; ">const</span><span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>checkBox<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span>
        <span style="color:#800000; font-weight:bold; ">return</span> <span style="color:#800000; font-weight:bold; ">true</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">return</span> <span style="color:#800000; font-weight:bold; ">false</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>
</pre>
 
 ## remtache.ui
 
![image](https://user-images.githubusercontent.com/86810485/150679916-6a4a2950-dc6a-44b4-913a-3f17ad350f25.png)


## MVC Model

Once you finished the first version, Try to move on to more complicated model using either

  * QTableView
  
  * QAbstractTableModel
  
  * QSqlTableModel

## Inhancements.

 * Try to add functionality to move task between views (for elites)

## tache.h

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">ifndef</span><span style="color:#004a43; "> TACHE_H</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">define</span><span style="color:#004a43; "> TACHE_H</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QWidget</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QAction</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMainWindow</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QListView</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMenu</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QToolBar</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QLabel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QStatusBar</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QSplitter</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QListWidget</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QStandardItemModel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QCloseEvent</span><span style="color:#800000; ">&gt;</span>

QT_BEGIN_NAMESPACE
<span style="color:#800000; font-weight:bold; ">namespace</span> Ui <span style="color:#800080; ">{</span> <span style="color:#800000; font-weight:bold; ">class</span> Tache<span style="color:#800080; ">;</span> <span style="color:#800080; ">}</span>
QT_END_NAMESPACE

<span style="color:#800000; font-weight:bold; ">class</span> Tache <span style="color:#800080; ">:</span> <span style="color:#800000; font-weight:bold; ">public</span> <span style="color:#603000; ">QMainWindow</span>
<span style="color:#800080; ">{</span>
    <span style="color:#004a43; ">Q_OBJECT</span>

<span style="color:#800000; font-weight:bold; ">public</span><span style="color:#e34adc; ">:</span>
    Tache<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">nullptr</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#808030; ">~</span>Tache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
    Ui<span style="color:#800080; ">::</span>Tache <span style="color:#808030; ">*</span>ui<span style="color:#800080; ">;</span>
<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
    <span style="color:#800000; font-weight:bold; ">void</span> createMainWindow<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">void</span> createActions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>  <span style="color:#696969; ">// fonction pour creer les actions dde notre application</span>
    <span style="color:#800000; font-weight:bold; ">void</span> createMenus<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>  <span style="color:#696969; ">//fonction pour creer des menus</span>
    <span style="color:#800000; font-weight:bold; ">void</span> createToolBars<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">void</span> makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>



<span style="color:#800000; font-weight:bold; ">public slots</span><span style="color:#e34adc; ">:</span>
     <span style="color:#800000; font-weight:bold; ">void</span> help<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
     <span style="color:#800000; font-weight:bold; ">void</span> newTache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800000; font-weight:bold; ">protected</span><span style="color:#e34adc; ">:</span>
     <span style="color:#800000; font-weight:bold; ">void</span> closeEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QCloseEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span> override<span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
     <span style="color:#603000; ">QStringList</span> sizeTaskToday<span style="color:#800080; ">;</span>
     <span style="color:#603000; ">QStringList</span> sizeTaskDone<span style="color:#800080; ">;</span>
     <span style="color:#603000; ">QStringList</span> sizeTaskFutur<span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">private</span><span style="color:#e34adc; ">:</span>
     <span style="color:#603000; ">QStandardItemModel</span> <span style="color:#808030; ">*</span>today<span style="color:#800080; ">;</span>
     <span style="color:#603000; ">QStandardItemModel</span> <span style="color:#808030; ">*</span>done<span style="color:#800080; ">;</span>
     <span style="color:#603000; ">QStandardItemModel</span> <span style="color:#808030; ">*</span>futur<span style="color:#800080; ">;</span>

<span style="color:#800000; font-weight:bold; ">public</span><span style="color:#e34adc; ">:</span>


<span style="color:#696969; ">//    QListWidget *listVToday;</span>
<span style="color:#696969; ">//    QListWidget *listVFutur;</span>
<span style="color:#696969; ">//    QListWidget *listVDone;</span>


    <span style="color:#696969; ">//definir pointeur sur chaque action</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>quit<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>newFile<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>saveFile<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>recent<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>about<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>option1<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>option2<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>finished<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QAction</span> <span style="color:#808030; ">*</span>pending<span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//definir les menus de l'application</span>
    <span style="color:#603000; ">QMenu</span> <span style="color:#808030; ">*</span>file<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QMenu</span> <span style="color:#808030; ">*</span>option<span style="color:#800080; ">;</span>
    <span style="color:#603000; ">QMenu</span> <span style="color:#808030; ">*</span>helpe<span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span><span style="color:#800080; ">;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">endif</span><span style="color:#004a43; "> </span><span style="color:#696969; ">// TACHE_H</span>
</pre>

## tache.cpp

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">tache.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">ui_tache.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">remtache.h</span><span style="color:#800000; ">"</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QSplitter</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMenu</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QListView</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QListWidget</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QHBoxLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QFileSystemModel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QAbstractItemModel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QStringListModel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QToolBar</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QApplication</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QHBoxLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QVBoxLayout</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMenuBar</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QPixmap</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QMessageBox</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QDate</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QFile</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QStandardItemModel</span><span style="color:#800000; ">&gt;</span>
<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QTextStream</span><span style="color:#800000; ">&gt;</span>

Tache<span style="color:#800080; ">::</span>Tache<span style="color:#808030; ">(</span><span style="color:#603000; ">QWidget</span> <span style="color:#808030; ">*</span>parent<span style="color:#808030; ">)</span>
    <span style="color:#800080; ">:</span> <span style="color:#603000; ">QMainWindow</span><span style="color:#808030; ">(</span>parent<span style="color:#808030; ">)</span>
    <span style="color:#808030; ">,</span> ui<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">new</span> Ui<span style="color:#800080; ">::</span>Tache<span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setupUi<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    today <span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QStandardItemModel</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    done <span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QStandardItemModel</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    futur <span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QStandardItemModel</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    createMainWidget<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    createActions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    createMenus<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    createToolBars<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//declaration du fichier</span>
    <span style="color:#603000; ">QFile</span> fichierTaches<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">C:/Users/med amine/OneDrive/Bureau/Documents/Database for Tasks/lesTaches.txt</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">if</span> <span style="color:#808030; ">(</span><span style="color:#808030; ">!</span>fichierTaches<span style="color:#808030; ">.</span>open<span style="color:#808030; ">(</span><span style="color:#603000; ">QIODevice</span><span style="color:#800080; ">::</span>ReadOnly <span style="color:#808030; ">|</span> <span style="color:#603000; ">QIODevice</span><span style="color:#800080; ">::</span>Text<span style="color:#808030; ">)</span><span style="color:#808030; ">)</span>
            <span style="color:#800000; font-weight:bold; ">return</span><span style="color:#800080; ">;</span>

        <span style="color:#800000; font-weight:bold; ">while</span> <span style="color:#808030; ">(</span><span style="color:#808030; ">!</span>fichierTaches<span style="color:#808030; ">.</span>atEnd<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span> <span style="color:#800080; ">{</span>
            <span style="color:#603000; ">QString</span> line <span style="color:#808030; ">=</span> fichierTaches<span style="color:#808030; ">.</span>readLine<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#603000; ">QStandardItem</span> <span style="color:#808030; ">*</span>t <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QStandardItem</span><span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


            <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>line<span style="color:#808030; ">.</span>at<span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">1</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

                sizeTaskToday<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>line<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/new_file.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span>line<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                today<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskToday<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>today<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span><span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>line<span style="color:#808030; ">.</span>at<span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">2</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

                sizeTaskFutur<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>line<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/pending_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span>line<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                futur<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskFutur<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>futur<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span><span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>line<span style="color:#808030; ">.</span>at<span style="color:#808030; ">(</span><span style="color:#008c00; ">0</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">3</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
                sizeTaskDone<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>line<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/finished_task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span>line<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                done<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskDone<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>done<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span>
        <span style="color:#800080; ">}</span>


<span style="color:#800080; ">}</span>

Tache<span style="color:#800080; ">::</span><span style="color:#808030; ">~</span>Tache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> ui<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> quit<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> newFile<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> saveFile<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> recent<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> about<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> option1<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> option2<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> finished<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> pending<span style="color:#800080; ">;</span>

    <span style="color:#800000; font-weight:bold; ">delete</span> file<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> option<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">delete</span> helpe<span style="color:#800080; ">;</span>



<span style="color:#800080; ">}</span>
<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>createMainWidget<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>createActions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

    <span style="color:#696969; ">//--&gt;  creer l'action new file</span>
    <span style="color:#603000; ">QPixmap</span> newIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/new_file.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    newFile<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>newIcon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;New File</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    newFile<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+N</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#696969; ">//connect(newFile,&amp;QAction::triggered, this, &amp;QMainWindow::create);</span>


    <span style="color:#696969; ">//--&gt;  creer l'action de finished task</span>
    <span style="color:#603000; ">QPixmap</span> finishedTaskIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/finished_task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    finished<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>finishedTaskIcon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> &amp;Finished Task</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    finished<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+F</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//--&gt;  creer l'action de pending task</span>
    <span style="color:#603000; ">QPixmap</span> pendingTaskIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/pending_task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    pending<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>pendingTaskIcon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> &amp;Pending Task</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    pending<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+P</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//--&gt;  creer l'action de save</span>
    <span style="color:#603000; ">QPixmap</span> saveIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/save_file.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    saveFile<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>saveIcon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> &amp;Save File</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    saveFile<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+S</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>


    <span style="color:#696969; ">//--&gt;  creer l'action de quit</span>
    <span style="color:#603000; ">QPixmap</span> quitIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/quit_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    quit <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>quitIcon<span style="color:#808030; ">,</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;Exit</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    quit<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+Q</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#696969; ">//connect(quit, &amp;QAction::triggered, this, &amp;QMainWindow::close);</span>


    <span style="color:#696969; ">//--&gt;  creer l'action about</span>
    <span style="color:#603000; ">QPixmap</span> aboutIcon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/about_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    about<span style="color:#808030; ">=</span><span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>aboutIcon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;About Us</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    about<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setShortcut<span style="color:#808030; ">(</span><span style="color:#400000; ">tr</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">Ctrl+A</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#696969; ">//connect(about, &amp;QAction::triggered, this, &amp;Taches::help);</span>

    <span style="color:#696969; ">//--&gt;  creation de l'action de option1 et option2</span>
    <span style="color:#603000; ">QPixmap</span> option1Icon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/option1_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    option1 <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>option1Icon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;Option 1</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#603000; ">QPixmap</span> option2Icon<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/option2_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    option2 <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QAction</span><span style="color:#808030; ">(</span>option2Icon<span style="color:#808030; ">,</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;Option 2</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>createMenus<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//definir le menu de notre application</span>
    file<span style="color:#808030; ">=</span>menuBar<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addMenu<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;File</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>newFile<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>saveFile<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>finished<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>pending<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    file<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>quit<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    menuBar<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    option <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QMenu</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;Options</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    option<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>option1<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    option<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>option2<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    menuBar<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addMenu<span style="color:#808030; ">(</span>option<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    menuBar<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    helpe <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QMenu</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;Help</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    helpe<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>about<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    menuBar<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addMenu<span style="color:#808030; ">(</span>helpe<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>createToolBars<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

    <span style="color:#696969; ">//creer un toolbar</span>
    <span style="color:#800000; font-weight:bold; ">auto</span> toolbar1 <span style="color:#808030; ">=</span>addToolBar<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">&amp;File1</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//ajouter des actions a ce toolbar</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>newFile<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>finished<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>pending<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addSeparator<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    toolbar1<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>addAction<span style="color:#808030; ">(</span>quit<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>makeConnexions<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

    <span style="color:#696969; ">//connetion for new file</span>
    <span style="color:#400000; ">connect</span><span style="color:#808030; ">(</span>newFile<span style="color:#808030; ">,</span><span style="color:#808030; ">&amp;</span><span style="color:#603000; ">QAction</span><span style="color:#800080; ">::</span>triggered<span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">&amp;</span>Tache<span style="color:#800080; ">::</span>newTache<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//connection for about</span>
    <span style="color:#400000; ">connect</span><span style="color:#808030; ">(</span>about<span style="color:#808030; ">,</span><span style="color:#808030; ">&amp;</span><span style="color:#603000; ">QAction</span><span style="color:#800080; ">::</span>triggered<span style="color:#808030; ">,</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">,</span><span style="color:#808030; ">&amp;</span>Tache<span style="color:#800080; ">::</span>help<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//connection for the exit button</span>
    <span style="color:#400000; ">connect</span><span style="color:#808030; ">(</span>quit<span style="color:#808030; ">,</span> <span style="color:#808030; ">&amp;</span><span style="color:#603000; ">QAction</span><span style="color:#800080; ">::</span>triggered<span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">,</span> <span style="color:#808030; ">&amp;</span>Tache<span style="color:#800080; ">::</span>close<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>help<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
   <span style="color:#603000; ">QMessageBox</span><span style="color:#800080; ">::</span>about<span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">this</span><span style="color:#808030; ">,</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">About Us</span><span style="color:#800000; ">"</span><span style="color:#808030; ">,</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">Groupe composer de Mohamed Amine Kebdani et Rania Touiham de la filiere Web et Mobile</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>

<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>newTache<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    remTache R<span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">auto</span> D<span style="color:#808030; ">=</span> R<span style="color:#808030; ">.</span>exec<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>D<span style="color:#808030; ">=</span><span style="color:#808030; ">=</span>remTache<span style="color:#800080; ">::</span>Accepted<span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
            <span style="color:#603000; ">QString</span> text <span style="color:#808030; ">=</span> R<span style="color:#808030; ">.</span>getDescription<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#603000; ">QStandardItem</span> <span style="color:#808030; ">*</span>t <span style="color:#808030; ">=</span> <span style="color:#800000; font-weight:bold; ">new</span> <span style="color:#603000; ">QStandardItem</span><span style="color:#800080; ">;</span>


            <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>R<span style="color:#808030; ">.</span>getDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">=</span><span style="color:#808030; ">=</span><span style="color:#603000; ">QDate</span><span style="color:#800080; ">::</span>currentDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">&amp;</span><span style="color:#808030; ">&amp;</span> <span style="color:#808030; ">!</span>R<span style="color:#808030; ">.</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">1 </span><span style="color:#800000; ">"</span><span style="color:#808030; ">+</span>text<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                today<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskToday<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>today<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                sizeTaskToday<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>text<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//            ui-&gt;sizeTasktoday-&gt;addItem(new QListWidgetItem(TodayIcon,text));</span>
            <span style="color:#800080; ">}</span>
            <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>R<span style="color:#808030; ">.</span>getDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">!</span><span style="color:#808030; ">=</span><span style="color:#603000; ">QDate</span><span style="color:#800080; ">::</span>currentDate<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#808030; ">&amp;</span><span style="color:#808030; ">&amp;</span> <span style="color:#808030; ">!</span>R<span style="color:#808030; ">.</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/pending_task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">2 </span><span style="color:#800000; ">"</span><span style="color:#808030; ">+</span>text<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                futur<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskFutur<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>futur<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                sizeTaskFutur<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>text<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//            ui-&gt;sizeTaskFutur-&gt;addItem(new QListWidgetItem(pendingIcon,text));</span>
            <span style="color:#800080; ">}</span>
            <span style="color:#800000; font-weight:bold; ">else</span> <span style="color:#800000; font-weight:bold; ">if</span><span style="color:#808030; ">(</span>R<span style="color:#808030; ">.</span>isChecked<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>
    <span style="color:#696969; ">//            QIcon completedIcon(":/icons/finished_task_icon.png");</span>

                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setIcon<span style="color:#808030; ">(</span><span style="color:#603000; ">QIcon</span><span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">:/icons/finished_task_icon.png</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                t<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setText<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">3 </span><span style="color:#800000; ">"</span><span style="color:#808030; ">+</span>text<span style="color:#808030; ">+</span><span style="color:#800000; ">"</span><span style="color:#0000e6; "> </span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                done<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>appendRow<span style="color:#808030; ">(</span>t<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

                ui<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>sizeTaskDone<span style="color:#808030; ">-</span><span style="color:#808030; ">&gt;</span>setModel<span style="color:#808030; ">(</span>done<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
                sizeTaskDone<span style="color:#808030; ">.</span>append<span style="color:#808030; ">(</span>text<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>

    <span style="color:#696969; ">//            ui-&gt;sizeTaskDone-&gt;addItem(new QListWidgetItem(completedIcon,text));</span>
            <span style="color:#800080; ">}</span>
        <span style="color:#800080; ">}</span>
<span style="color:#800080; ">}</span>
<span style="color:#800000; font-weight:bold; ">void</span> Tache<span style="color:#800080; ">::</span>closeEvent<span style="color:#808030; ">(</span><span style="color:#603000; ">QCloseEvent</span> <span style="color:#808030; ">*</span>e<span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#603000; ">QFile</span> fichierTaches<span style="color:#808030; ">(</span><span style="color:#800000; ">"</span><span style="color:#0000e6; ">C:/Users/med amine/OneDrive/Bureau/Documents/Database for Tasks/lesTaches.txt</span><span style="color:#800000; ">"</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800000; font-weight:bold; ">if</span> <span style="color:#808030; ">(</span>fichierTaches<span style="color:#808030; ">.</span>open<span style="color:#808030; ">(</span><span style="color:#603000; ">QIODevice</span><span style="color:#800080; ">::</span>ReadWrite<span style="color:#808030; ">|</span> <span style="color:#603000; ">QIODevice</span><span style="color:#800080; ">::</span>Text<span style="color:#808030; ">)</span><span style="color:#808030; ">)</span><span style="color:#800080; ">{</span>

            <span style="color:#603000; ">QTextStream</span> out<span style="color:#808030; ">(</span><span style="color:#808030; ">&amp;</span>fichierTaches<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
            <span style="color:#800000; font-weight:bold; ">for</span> <span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>i<span style="color:#808030; ">&lt;</span>sizeTaskToday<span style="color:#808030; ">.</span>size<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800080; ">;</span>i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span> <span style="color:#808030; ">)</span> <span style="color:#800080; ">{</span>
                out<span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">1</span><span style="color:#800000; ">"</span><span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> sizeTaskToday<span style="color:#808030; ">[</span>i<span style="color:#808030; ">]</span> <span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span><span style="color:#603000; ">endl</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span>
            <span style="color:#800000; font-weight:bold; ">for</span> <span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>i<span style="color:#808030; ">&lt;</span>sizeTaskFutur<span style="color:#808030; ">.</span>size<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800080; ">;</span>i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span> <span style="color:#808030; ">)</span> <span style="color:#800080; ">{</span>
                out<span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">2</span><span style="color:#800000; ">"</span><span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> sizeTaskFutur<span style="color:#808030; ">[</span>i<span style="color:#808030; ">]</span> <span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span><span style="color:#603000; ">endl</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span>
            <span style="color:#800000; font-weight:bold; ">for</span> <span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> i<span style="color:#808030; ">=</span><span style="color:#008c00; ">0</span><span style="color:#800080; ">;</span>i<span style="color:#808030; ">&lt;</span>sizeTaskDone<span style="color:#808030; ">.</span>size<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span> <span style="color:#800080; ">;</span>i<span style="color:#808030; ">+</span><span style="color:#808030; ">+</span> <span style="color:#808030; ">)</span> <span style="color:#800080; ">{</span>
                out<span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#800000; ">"</span><span style="color:#0000e6; ">3</span><span style="color:#800000; ">"</span><span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> sizeTaskDone<span style="color:#808030; ">[</span>i<span style="color:#808030; ">]</span> <span style="color:#808030; ">&lt;</span><span style="color:#808030; ">&lt;</span> <span style="color:#666616; ">Qt</span><span style="color:#800080; ">::</span><span style="color:#603000; ">endl</span><span style="color:#800080; ">;</span>
            <span style="color:#800080; ">}</span>
            fichierTaches<span style="color:#808030; ">.</span>close<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
        <span style="color:#800080; ">}</span>
<span style="color:#800080; ">}</span>
</pre>


## tache.ui

![image](https://user-images.githubusercontent.com/86810485/150681507-3c96ca89-ee96-46f6-a9d1-90651d9d6e04.png)

 ## main.cpp

<pre style="color:#000000;background:#ffffff;"><span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">"</span><span style="color:#40015a; ">tache.h</span><span style="color:#800000; ">"</span>

<span style="color:#004a43; ">#</span><span style="color:#004a43; ">include </span><span style="color:#800000; ">&lt;</span><span style="color:#40015a; ">QApplication</span><span style="color:#800000; ">&gt;</span>

<span style="color:#800000; font-weight:bold; ">int</span> <span style="color:#400000; ">main</span><span style="color:#808030; ">(</span><span style="color:#800000; font-weight:bold; ">int</span> argc<span style="color:#808030; ">,</span> <span style="color:#800000; font-weight:bold; ">char</span> <span style="color:#808030; ">*</span>argv<span style="color:#808030; ">[</span><span style="color:#808030; ">]</span><span style="color:#808030; ">)</span>
<span style="color:#800080; ">{</span>
    <span style="color:#603000; ">QApplication</span> a<span style="color:#808030; ">(</span>argc<span style="color:#808030; ">,</span> argv<span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    Tache w<span style="color:#800080; ">;</span>
    w<span style="color:#808030; ">.</span>show<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
    <span style="color:#800000; font-weight:bold; ">return</span> a<span style="color:#808030; ">.</span>exec<span style="color:#808030; ">(</span><span style="color:#808030; ">)</span><span style="color:#800080; ">;</span>
<span style="color:#800080; ">}</span>
</pre>


## fichier resource

![image](https://user-images.githubusercontent.com/86810485/150681638-03d3da2d-9628-4165-bcd9-9c6f2ec89cd3.png)

## compilation

![image](https://user-images.githubusercontent.com/86810485/150682365-3b959ff1-2fd6-4ddf-b159-6ffe88e11cd7.png)

## fichier test 

![image](https://user-images.githubusercontent.com/86810485/150682732-6e9f0220-b7f6-4086-97ff-a31fb88f44d1.png)


       
       
       
       
       
