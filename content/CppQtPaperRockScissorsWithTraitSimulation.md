
 

 

 

 

 

([C++](Cpp.md)) [QtPaperRockScissorsWithTraitSimulation](CppQtPaperRockScissorsWithTraitSimulation.md)
========================================================================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppQtPaperRockScissorsWithTraitSimulation/CppQtPaperRockScissorsWithTraitSimulation.pri
-----------------------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtPaperRockScissorsWithTraitSimulation  SOURCES += \     ../../Classes/CppQtPaperRockScissorsWithTraitSimulation/qtpaperrockscissorswithtraitwidget.cpp  HEADERS  += \     ../../Classes/CppQtPaperRockScissorsWithTraitSimulation/qtpaperrockscissorswithtraitwidget.h  FORMS  += \     ../../Classes/CppQtPaperRockScissorsWithTraitSimulation/qtpaperrockscissorswithtraitwidget.ui  OTHER_FILES += \     ../../Classes/CppQtPaperRockScissorsWithTraitSimulation/Licence.txt`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtPaperRockScissorsWithTraitSimulation/qtpaperrockscissorswithtraitwidget.h
--------------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTPAPERROCKSCISSORSWITHTRAITWIDGET_H #define QTPAPERROCKSCISSORSWITHTRAITWIDGET_H  #include <QWidget> #include <QPixmap>  #include "paperrockscissorswithtraitsimulation.h" #include "paperrockscissorswithtraitinitialization.h"  namespace Ui {   class QtPaperRockScissorsWithTraitWidget; }  struct QImage;  class QtPaperRockScissorsWithTraitWidget : public QWidget {   Q_OBJECT  public:   using Init = ribi::prswt::Initialization;    explicit QtPaperRockScissorsWithTraitWidget(     const int width = 600,     const int height = 400,     const Init initialization = Init::random,     const int rng_seed = 42,     QWidget *parent = 0   );   QtPaperRockScissorsWithTraitWidget(const QtPaperRockScissorsWithTraitWidget&) = delete;   QtPaperRockScissorsWithTraitWidget& operator=(const QtPaperRockScissorsWithTraitWidget&) = delete;   ~QtPaperRockScissorsWithTraitWidget();    std::tuple<int,int,int> GetLastPopSizes() const;   std::tuple<double,double,double> GetLastMeanTraits() const;    void SetAll(     const int width,     const int height,     const Init initialization,     const int rng_seed   );    static QRgb ToRgb(const ribi::PaperRockScissors prs) noexcept;  protected:   void paintEvent(QPaintEvent *); private:   Ui::QtPaperRockScissorsWithTraitWidget *ui;   QPixmap m_pixmap;   ribi::prswt::Simulation m_simulation;  private slots:   void OnTimer();  signals:   //Emitted everytime OnTimer is run   void signal_next(); };   #endif // QTPAPERROCKSCISSORSWITHTRAITWIDGET_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtPaperRockScissorsWithTraitSimulation/qtpaperrockscissorswithtraitwidget.cpp
----------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtpaperrockscissorswithtraitwidget.h"  #include <cassert>  #include <QImage> #include <QPainter> #include <QPixmap> #include <QTimer>  #include "paperrockscissorswithtraitparameters.h" #include "paperrockscissorswithtraitsimulation.h" #include "ui_qtpaperrockscissorswithtraitwidget.h"  QtPaperRockScissorsWithTraitWidget::QtPaperRockScissorsWithTraitWidget(   const int width,   const int height,   const Init initialization,   const int rng_seed,   QWidget *parent )   : QWidget(parent),     ui(new Ui::QtPaperRockScissorsWithTraitWidget),     m_pixmap(width,height),     m_simulation(ribi::prswt::Parameters(width,height,initialization,rng_seed)) {   ui->setupUi(this);   OnTimer();   //Start a timer   {     QTimer * const timer{new QTimer(this)};     QObject::connect(timer,SIGNAL(timeout()),this,SLOT(OnTimer()));     timer->setInterval(100);     timer->start();   } }  QtPaperRockScissorsWithTraitWidget::~QtPaperRockScissorsWithTraitWidget() {   delete ui; }  std::tuple<int,int,int> QtPaperRockScissorsWithTraitWidget::GetLastPopSizes() const {   return m_simulation.GetLastPopSizes(); }  std::tuple<double,double,double> QtPaperRockScissorsWithTraitWidget::GetLastMeanTraits() const {   return m_simulation.GetLastMeanTraits(); }  void QtPaperRockScissorsWithTraitWidget::OnTimer() {   m_simulation.Next();    const int height{m_pixmap.height()};   const int width{m_pixmap.width()};   QImage image(width,height,QImage::Format_RGB32);   const auto& grid = m_simulation.GetGrid();   for (int y=0; y!=height; ++y)   {     const auto line = grid[y];     for (int x=0; x!=width; ++x)     {       const auto cell = line[x];       image.setPixel(x,y,ToRgb(cell.GetPrs()));     }   }   m_pixmap = QPixmap::fromImage(image);   update();    emit signal_next(); }  void QtPaperRockScissorsWithTraitWidget::paintEvent(QPaintEvent *) {   QPainter painter(this);   painter.drawPixmap(     this->rect(),     m_pixmap   ); }  void QtPaperRockScissorsWithTraitWidget::SetAll(   const int width,   const int height,   const Init initialization,   const int rng_seed ) {   m_pixmap = QPixmap(width,height);   m_simulation = ribi::prswt::Simulation(     ribi::prswt::Parameters(       width,       height,       initialization,       rng_seed     )   );   update(); }  QRgb QtPaperRockScissorsWithTraitWidget::ToRgb(const ribi::PaperRockScissors prs) noexcept {   using Prs = ribi::PaperRockScissors;   const int brightness{196};   switch (prs)   {     case Prs::paper: return qRgb(0,0,brightness);     case Prs::rock: return qRgb(brightness,0,0);     case Prs::scissors: return qRgb(0,brightness,0);   }   assert(!"Should not get here");   throw std::logic_error("QtPaperRockScissorsWithTraitWidget::ToColor: unknown value of prs"); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

