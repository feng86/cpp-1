
 

 

 

 

 

([C++](Cpp.md)) ![Qt](PicQt.png) [How to resize a dialog?](CppQtResizeDialog.md)
==================================================================================

 

There are multiple options:

1.  this-&gt;resize(int any\_width,int any\_height)
2.  this-&gt;setGeometry(int any\_left, int any\_right, int
    any\_width,int any\_height)
3.  this-&gt;setGeometry(QRect any\_rect)

Resize [this](CppThis.md) in a [member function](CppMemberFunction.md)
of the dialog.

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "dialog.h" #include "ui_dialog.h"  Dialog::Dialog(QWidget *parent) :     QDialog(parent),     ui(new Ui::Dialog) {   ui->setupUi(this);   //Resize the dialog to 100x100 pixels   this->resize(100,100); }  Dialog::~Dialog() {   delete ui; }  void Dialog::changeEvent(QEvent *e) {   QDialog::changeEvent(e);   switch (e->type()) {   case QEvent::LanguageChange:     ui->retranslateUi(this);     break;   default:     break;   } }  void Dialog::resizeEvent(QResizeEvent*) {   static int n_times = 0;   QString s; s = s.number(n_times);   ui->label->setText("Resized " + s + " times");   ++n_times; }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

[Example 10](CppQtExample10.md) shows how to implement a resize event.

 

 

 

 

 

