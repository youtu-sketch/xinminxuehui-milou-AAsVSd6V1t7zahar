
## 0\.前言


我想通过编写一个完整的游戏程序方式引导读者体验程序设计的全过程。我将采用多种方式编写具有相同效果的应用程序，并通过不同方式形成的代码和实现方法的对比来理解程序开发更深层的知识。


了解我编写教程的思路，请参阅体现我最初想法的那篇文章中的“1\.编程计划”：


[学习编程从游戏开始 \- lexyao \- 博客园](https://github.com)


了解不同方式实现同样效果的差异，请阅读以下文章：


* [在CodeBolcks\+wxWidgets下的C\+\+编程教程——用向导创建一个wxWidgets项目（xTetris） \- lexyao \- 博客园](https://github.com)
* [在CodeBolcks\+wxWidgets\+wxSmith下的C\+\+编程教程——用向导创建一个wxWidgets项目（sTetris） \- lexyao \- 博客园](https://github.com)


在这篇文章里，我主要讲述以下几个方面的内容：


1. 使用向导新建一个wxWidgets程序（sTetris）
2. 向导为我生成的项目文件sTetris与xTetris有什么不同
3. 通过修改sTetris的代码实现与xTetris一致的视觉效果
4. 使用wxSmith修改sTetris实现与xTetris一致的视觉效果
5. 结束语


 


## 1\.使用向导新建一个wxWidgets程序（sTetris）


在开始下面的内容之前，我假定你已经安装了CodeBlocks程序开发环境，配置了wxWidgets，测试使用CodeBlocks创建第一个程序成功编译运行，并且了解了C\+\+语言的基础知识和使用wxWiddgets开发C\+\+程序的知识。


如果你还有哪一方面没有做到，请阅读下面的文章：


* [体验Code::Blocks下的C\+\+编程 \- lexyao \- 博客园](https://github.com)：搭设Code::Blocks开发平台（安装）
* [在Windows下为CodeBlocks20\.3安装、配置wxWidget3\.2\.6 \- lexyao \- 博客园](https://github.com):[wgetcloud全球加速器服务](https://wgetcloud6.org)：安装、编译、配置wxWidget，测试在CodeBlocks中使用wxWidget编写的第一个程序
* [wxWidgets 跨平台 GUI 编程](https://github.com)：系统地讲述使用wxWiddgets开发C\+\+程序的知识
* [C 语言教程 \| 菜鸟教程](https://github.com)：系统地讲述C语言编程的基础知识
* [C\+\+ 教程 \| 菜鸟教程](https://github.com)：系统地讲述C\+\+语言编程的基础知识


在开始下面的内容之前，你还需要阅读我写的以下文章。在以下文章中有创建应用程序xTetris的全部内容，而本篇文章中创建应用程序sTetris的过程、解读、修改等都要与xTetris进行对比，认识二者的异同点。


[在CodeBolcks\+wxWidgets下的C\+\+编程教程——用向导创建一个wxWidgets项目（xTetris） \- lexyao \- 博客园](https://github.com)


使用向导新建一个wxWidgets程序的操作步骤如下：


第一步：打开新建项目向导


创建任何类型的项目在这一步的操作是相同的，后续就有差别了。有两种方法：


①主菜单：File\-\>New\-\>Projects


②点击Start Here页面中的Create New Project


第二步：在窗口中选择项目类型wxWidgets project


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241210212754989-208398921.png)


 第三步、按向导的提示完成创建项目的过程


我重点介绍几个向导界面，没有介绍的向导页面你直接点击Next按钮就行了。


阅读下面的内容时重点关注与创建xTetris时不一样的地方。


向导页面①：


选择wxWidgets  3\.2\.x。选择哪一个版本要看你安装的是哪一个版本的wxWidgets 库文件，选择了你没有的版本，在编译你的程序时会因为找不到库文件而导致编译失败。


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241210213110199-1299267104.png)


 向导页面②：输入项目名称。将来你编译生成的exe应用程序将会使用这个名称。保存这个项目的文件夹也会默认使用这个名称，不过你可以在这个页面中修改保存项目文件的文件夹。


* 在项目名称栏中输入sTetris。将来编译生成的项目文件将会是xTetris.exe
* 将文件路径中自动添加的sTetris改为Tetris。修改之后保存创建的项目文件的文件夹将会是Tetris，而不是默认的sTetris


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241211221710959-1917925475.png)


 


  向导页面③：


在Preferred GUl Builder栏目中选择编写程序时构建GUI界面使用的方法。在这个项目中选择wxSmith，将来在项目中使用wxSmith构建GUI界面。


在Application Type栏目中选择应用程序的类型。在这个项目中选择Frame Based，也就是说要基于wxFrame创建你的应用程序的主界面。


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241211221848404-1741713050.png)


  向导页面④：


在wxWidgets Library Settings栏目中选择wxWidgets库文件的设置。


这是一组多选项，你可以选择其中的任意一个或多个，但你选择的必须是可用的。这一组选项中的每一个选项都对应着你编译wxWidgets库文件时使用的命令行参数。


由于我在编译wxWidgets库文件时的命令行参数使用了SHARED\=0 MONOLITHIC\=1 UNICODE\=1，所以我必须选中wxWidgets is built as a monolithic library和Enable unicode，而不能选中Use wxWidgets DLL。


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241210222133697-536611638.png)


 按向导完成项目创建后，在CodeBlocks左边的栏目中将会看到新创建项目所包含的文件。下图中显示了向导创建的项目中包含的文件的清单。


你可以在文件资源管理器中打开前面在“向导页面②”看到的保存项目文件的文件夹你会看到里面有向导创建的文件。


 ![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241211221941049-2083919261.png)


 


为了与今后将要创建的项目文件名称有区别，将向导生成的资源文件的文件名由resource.rc改为sTetris.rc。


修改文件名的操作方法是：


在CodeBlocks左边的栏目中要修改的文件名上点击鼠标右键，从弹出的菜单中选择“Rename file…”，输入新的文件名，点击\[OK]按钮确认修改。


完成修改后你会发现CodeBlocks左边的栏目中的文件变成了新的文件名，文件资源管理器中的文件名也同步改变了。


在文件资源管理器中你看到了sTetris和xTetris两个项目的文件都放在了同一个文件夹中。在这个文件夹中还增加了一个名为wxsmith的文件夹，在这个文件夹中保存着sTetrisframe.wxs文件，这正是sTetris比xTetris多出的那个文件。


 第四步、编译运行创建的项目


Code::Blocks工具栏中的编译运行按钮，就会执行编译过程。Code::Blocks下部的窗口中有两个选项卡，分别是编译日志和编译信息。如果编译出错，会在这里出现红色的错误信息。如果是代码错误，编译结束后，点击错误信息，代码窗口会跳转到出错的代码行。


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241211120951669-1910338555.png)


 只要不出现错误，编译链接完成后就会运行程序，出现你的应用程序运行后的主界面窗口。


以下是基于wxFrame创建的应用程序的主界面，这个例子中在向导的选择GUI构建方式时，选择了wxSmith。


 ![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241210225231137-1925013938.png) 


## 2\.向导为我生成的项目文件sTetris与xTetris有什么不同


同样是使用向导生成的项目，只是选择了不同的界面构建方法，生成的文件有什么不同呢？下面我们逐个看一看。在阅读下面的内容时，你可能需要打开介绍创建xTetris的那个网页，需要对照阅读，查看有什么异同点。


### 2\.1 资源文件sTetris.rc


用鼠标双击Code Blocks左边列表中的文件名sTetris.rc，Code Blocks右边的编辑区内便显示出这个文件的内容。通过对比你会发现，sTetris.rc与xTetris.rc的内容完全相同。




```
aaaa ICON "wx/msw/std.ico"

#include "wx/msw/wx.rc"
```


#### 2\.2 两个头文件sTetrisApp.h和sTetrisMain.h


sTetrisApp.h文件的代码如下。通过对比你会发现，除了与项目名称中的s与x的差别，sTetris.h与xTetris.h的内容完全相同。




```
#ifndef STETRISAPP_H
#define STETRISAPP_H

#include 

class sTetrisApp : public wxApp
{
    public:
        virtual bool OnInit();
};

#endif // STETRISAPP_H
```


sTetrisMain.h文件的代码如下。通过对比你会发现，除了与项目名称中的s与x的差别，不一样的地方增加了许多。


* 都定义了构造函数和析构函数，构造函数的参数不同
* 事件处理函数数量不同，sTetrisMain.h中的事件处理函数被//(\*Handlers(sTetrisFrame)……//\*)括起来
* 定义作为组件ID的常数的数量和方式都不同，但效果一致，sTetrisMain.h中的常量被//(\*Identifiers(sTetrisFrame)……//\*)括起来
* sTetrisMain.h中增加了状态条组件的定义，还使用//(\*Declarations(sTetrisFrame)……//\*)括起来
* 定义事件表的宏DECLARE\_EVENT\_TABLE




```
#ifndef STETRISMAIN_H
#define STETRISMAIN_H

//(*Headers(sTetrisFrame)
#include 
#include 
#include 
//*)

class sTetrisFrame: public wxFrame
{
    public:

        sTetrisFrame(wxWindow* parent,wxWindowID id = -1);
        virtual ~sTetrisFrame();

    private:

        //(*Handlers(sTetrisFrame)
        void OnQuit(wxCommandEvent& event);
        void OnAbout(wxCommandEvent& event);
        //*)

        //(*Identifiers(sTetrisFrame)
        static const long idMenuQuit;
        static const long idMenuAbout;
        static const long ID_STATUSBAR1;
        //*)

        //(*Declarations(sTetrisFrame)
        wxStatusBar* StatusBar1;
        //*)

        DECLARE_EVENT_TABLE()
};

#endif // STETRISMAIN_H
```


#### 2\.3 两个C\+\+源代码文件sTetrisApp.cpp和sTetrisMain.cpp


sTetrisApp.cpp文件的代码如下。


通过对比你会发现，除了与项目名称中的s与x的差别，不一样的地方增加了许多。


* sTetrisApp.cpp没有设置主窗口标题和图标
* sTetrisApp::OnInit中的代码被//(\*AppInitialize(sTetrisFrame)……//\*)括起来




```
#include "sTetrisApp.h"

//(*AppHeaders
#include "sTetrisMain.h"
#include 
//*)

IMPLEMENT_APP(sTetrisApp);

bool sTetrisApp::OnInit()
{
    //(*AppInitialize
    bool wxsOK = true;
    wxInitAllImageHandlers();
    if ( wxsOK )
    {
        sTetrisFrame* Frame = new sTetrisFrame(0);
        Frame->Show();
        SetTopWindow(Frame);
    }
    //*)
    return wxsOK;

}
```


sTetrisMain.cpp文件的代码如下。


通过对比你会发现，除了与项目名称中的s与x的差别，不一样的地方增加了许多。


* 事件处理函数的连接方式不同
* 组件创建的方式有所不同
* 多出代码代码被//(\*xxxxx(sTetrisFrame)……//\*)括起来，其中的xxxxx代表不同的标识符




```
#include "sTetrisMain.h"
#include 

//(*InternalHeaders(sTetrisFrame)
#include 
#include string.h>
//*)

//helper functions
enum wxbuildinfoformat {
    short_f, long_f };

wxString wxbuildinfo(wxbuildinfoformat format)
{
    wxString wxbuild(wxVERSION_STRING);

    if (format == long_f )
    {
#if defined(__WXMSW__)
        wxbuild << _T("-Windows");
#elif defined(__UNIX__)
        wxbuild << _T("-Linux");
#endif

#if wxUSE_UNICODE
        wxbuild << _T("-Unicode build");
#else
        wxbuild << _T("-ANSI build");
#endif // wxUSE_UNICODE
    }

    return wxbuild;
}

//(*IdInit(sTetrisFrame)
const long sTetrisFrame::idMenuQuit = wxNewId();
const long sTetrisFrame::idMenuAbout = wxNewId();
const long sTetrisFrame::ID_STATUSBAR1 = wxNewId();
//*)

BEGIN_EVENT_TABLE(sTetrisFrame,wxFrame)
    //(*EventTable(sTetrisFrame)
    //*)
END_EVENT_TABLE()

sTetrisFrame::sTetrisFrame(wxWindow* parent,wxWindowID id)
{
    //(*Initialize(sTetrisFrame)
    wxMenu* Menu1;
    wxMenu* Menu2;
    wxMenuBar* MenuBar1;
    wxMenuItem* MenuItem1;
    wxMenuItem* MenuItem2;

    Create(parent, id, wxEmptyString, wxDefaultPosition, wxDefaultSize, wxDEFAULT_FRAME_STYLE, _T("id"));
    MenuBar1 = new wxMenuBar();
    Menu1 = new wxMenu();
    MenuItem1 = new wxMenuItem(Menu1, idMenuQuit, _("Quit\tAlt-F4"), _("Quit the application"), wxITEM_NORMAL);
    Menu1->Append(MenuItem1);
    MenuBar1->Append(Menu1, _("&File"));
    Menu2 = new wxMenu();
    MenuItem2 = new wxMenuItem(Menu2, idMenuAbout, _("About\tF1"), _("Show info about this application"), wxITEM_NORMAL);
    Menu2->Append(MenuItem2);
    MenuBar1->Append(Menu2, _("Help"));
    SetMenuBar(MenuBar1);
    StatusBar1 = new wxStatusBar(this, ID_STATUSBAR1, 0, _T("ID_STATUSBAR1"));
    int __wxStatusBarWidths_1[1] = { -1 };
    int __wxStatusBarStyles_1[1] = { wxSB_NORMAL };
    StatusBar1->SetFieldsCount(1,__wxStatusBarWidths_1);
    StatusBar1->SetStatusStyles(1,__wxStatusBarStyles_1);
    SetStatusBar(StatusBar1);

    Connect(idMenuQuit,wxEVT_COMMAND_MENU_SELECTED,(wxObjectEventFunction)&sTetrisFrame::OnQuit);
    Connect(idMenuAbout,wxEVT_COMMAND_MENU_SELECTED,(wxObjectEventFunction)&sTetrisFrame::OnAbout);
    //*)
}

sTetrisFrame::~sTetrisFrame()
{
    //(*Destroy(sTetrisFrame)
    //*)
}

void sTetrisFrame::OnQuit(wxCommandEvent& event)
{
    Close();
}

void sTetrisFrame::OnAbout(wxCommandEvent& event)
{
    wxString msg = wxbuildinfo(long_f);
    wxMessageBox(msg, _("Welcome to..."));
}
```


从上面的代码中分析得出结论，凡是被//(\*xxxxx(sTetrisFrame)……//\*)括起来的代码都是wxSmith自动维护的，这是wxSmith的识别标志。


## 3\.通过修改sTetris的代码实现与xTetris一致的视觉效果


向导生成的项目sTetris和xTetris视觉效果不同的地方是有三点：标题、图标、状态栏。


要想实现视觉效果一致，需要给sTetris增加实现三方面的效果：


* 主窗口标题栏显示标题
* 主窗口左上角显示与任务栏中一样的图标
* 状态栏分成两列，还要显示文字


下面分别实现这三方面的效果。


### 3\.1 主窗口标题栏显示标题


在不了解程序中的实现方法的时候，查看已经存在的代码是最好的办法。这种方法在程序员的生涯中是经常使用的，自己不会的东西拥有别人会做，参照一下别人的做法，自己也就懂了，懂了之后是沿用别人的方法还是自己改进，那就看具体情况了。


关于窗口标题的显示，我有现成的例子。


第一步、找到xTetris项目中显示窗口标题的代码


xTetrisApp.cpp文件有我们曾经修改过的代码：




```
    xTetrisFrame* frame = new xTetrisFrame(0L, _T("多彩俄罗斯方块xTetris"));//wxWidgets Application Template
```


从代码看出，主窗口标题是在xTetrisFrame类的构造函数中设置的。


第二步、逆向查找


逆向查找的思路就是沿着代码继承的顺序逆向查找实现这项功能的代码。


具体到设置主窗口标题，那就是找到xTetrisFrame类的构造函数，沿着继承顺序继续往上找，顺藤摸瓜，直到找到设置窗口标题的最初的代码。


在打开的xTetrisApp.cpp文件中右击xTetrisFrame，从弹出菜单中分别选择“Find declaration of 'xTetrisFrame'”和“Find implementtaion of 'xTetrisFrame'”查找有用的代码，在后者中找到xTetrisFrame的构造函数的实现代码：




```
xTetrisFrame::xTetrisFrame(wxFrame *frame, const wxString& title)
    : wxFrame(frame, -1, title)
```


从代码看出，，对应主窗口标题的是构造函数中的参数title，下一步就是查找参数title最终的使用者。xTetrisFrame的构造函数是继承了wxFrame的构造函数，继续逆向查找，在wxFrame构造函数的定义中找到以下代码：



 // construction wxFrame() { Init(); } wxFrame(wxWindow \*parent, 　　　　wxWindowID id, 　　　　const wxString\& title, 　　　　const wxPoint\& pos \= wxDefaultPosition, 　　　　const wxSize\& size \= wxDefaultSize, 　　　　long style \= wxDEFAULT\_FRAME\_STYLE, 　　　　const wxString\& name \= wxASCII\_STR(wxFrameNameStr)) 　　{ 　　Init();


　　Create(parent, id, title, pos, size, style, name);


 　　}


 bool Create(wxWindow \*parent, 　　　　wxWindowID id, 　　　　const wxString\& title, 　　　　const wxPoint\& pos \= wxDefaultPosition, 　　　　const wxSize\& size \= wxDefaultSize, 　　　　long style \= wxDEFAULT\_FRAME\_STYLE, 　　　　const wxString\& name \= wxASCII\_STR(wxFrameNameStr)); virtual \~wxFrame();



有两处出现了title：


* wxFrame构造函数的参数：wxFrame构造函数的构造函数有多个参数，xTetrisFrame的构造函数只使用了其中的两个
* Create函数的参数：Create函数的参数跟wxFrame构造函数是一样的，这两个函数是为了以不同的方式创建wxFrame类的实例而设置的


第三步、对照查看sTetris中的代码有什么不一样


打开sTetrisApp.cpp文件找到构建代码：




```
     sTetrisFrame* Frame = new sTetrisFrame(0);
```


从代码看出，sTetrisFrame的构造函数中没有主窗口标题，参数个数比在xTetrisFrame类的构造函数少。


用上述方法找到sTetris中xTetrisFrame的构造函数，却发现通过右键菜单中的查找找不到，这是把代码用//(\*xxxxx(sTetrisFrame)……//\*)括起来造成的，Code Blocks理解为注释而不是代码。我们只能打开文件自己用笨办法查找了：



sTetrisFrame::sTetrisFrame(wxWindow\* parent,wxWindowID id){ 　　//(\*Initialize(sTetrisFrame) 　　……


 　　Create(parent, id, wxEmptyString, wxDefaultPosition, wxDefaultSize, wxDEFAULT\_FRAME\_STYLE, \_T("id"));


　　……


　　//\*);


}



从代码看出，sTetrisFrame的构造函数中也是通过调用Create函数实现的，而Create函数对应title参数的位置使用了wxEmptyString，也就是给它一个空字符串。


空字符串当然不会再标题中显示出内容了。这样就找到主窗口没有标题的原因了。


第四步、寻找解决方案


sTetrisFrame的构造函数中没有title参数，给它加上是不是可以呢？


这样修改也不是不可以，修改自己的sTetrisFrame构造函数又不影响wxWidgets的wxFrame的构造函数，不会影响其他程序的使用。


虽然是这么个理，但还要看添加的参数是怎么使用的。


从上面的代码中可以看出，Create是在//(\*Initialize(sTetrisFrame)……//\*)范围内使用的，这部分代码是wxSmith创建和维护的，如果修改了这部分代码，可能会导致wxSmith不能识别而产生灾难性的后果。


如果给sTetrisFrame的构造函数中添加了title参数，必须在//(\*Initialize(sTetrisFrame)……//\*)之外使用才不会影响wxSmith。


此路不通，则需要另寻思路。


既然程序中是通过wxFrame的构造函数设置主窗口标题，那么应该有设置标题的函数。


第五步、查找设置标题的函数


关闭CodeBlocks中所有打开的文件，只保留包含wxFrame类定义的头文件，然后按着wxFrame的继承顺序逆向打开所有父类的头文件。


使用主菜单\[Search\-\>Find in files...]在打开的头文件中查找title，然后在查找的结果中寻找感兴趣的条目，双击这个条目，跳转到这个条目所在的文件中，并定位在文件中出现这个条目的地方。


![](https://img2024.cnblogs.com/blog/93363/202412/93363-20241212111329848-870583393.png)


 查看这个函数是否在类定义的public范围内，如果是public的，在子类中就可以直接调用。




```
// ----------------------------------------------------------------------------
// wxTopLevelWindow: a top level (as opposed to child) window
// ----------------------------------------------------------------------------

class WXDLLIMPEXP_CORE wxTopLevelWindowBase : public wxNonOwnedWindow
{
public:
　　......
    // get the frame icon
    wxIcon GetIcon() const;

    // get the frame icons
    const wxIconBundle& GetIcons() const { return m_icons; }

    // set the frame icon: implemented in terms of SetIcons()
    void SetIcon(const wxIcon& icon);
    ......
    // the title of the top level window: the text which the
    // window shows usually at the top of the frame/dialog in dedicated bar
    virtual void SetTitle(const wxString& title) = 0;
    virtual wxString GetTitle() const = 0;    ......
```


这里找到的函数确实在public范围内，这样就可以在子类中使用了。


第六步、实现方法


sTetrisFrame是wxTopLevelWindowBase的子类，可以直接使用SetTitle设置主窗口标题，那么我们就有了两种解决方案。


第一个方案：在sTetrisFrame内部使用。


参照xTetrisFrame修改sTetrisFrame的构造函数，在参数中增加title参数，并在//(\*Initialize(sTetrisFrame)……//\*)之后使用SetTitle设置主窗口标题，这样就可以参照xTetris的方法设置主窗口标题了。


修改后的代码如下：


sTetrisMain.h文件：




```
class sTetrisFrame: public wxFrame
{
    public:

        sTetrisFrame(wxWindow* parent,const wxString& title,wxWindowID id = -1);
        ....
```


sTetrisMain.cpp文件：




```
sTetrisFrame::sTetrisFrame(wxWindow* parent,const wxString& title,wxWindowID id)
{
    //(*Initialize(sTetrisFrame)
    ......
    //*)
    SetTitle(title);
}
```


sTetrisApp.cpp文件：




```
     sTetrisFrame* Frame = new sTetrisFrame(0L, _T("多彩俄罗斯方块xTetris"));//sTetrisFrame* Frame = new sTetrisFrame(0);
```


 


 


对应主窗口标题的是构造函数中的参数title，下一步就是查找参数title最终的使用者。xTetrisFrame的构造函数是继承了wxFrame的构造函数，继续逆向查找，在wxFrame构造函数的定义中找到以下代码：


### 3\.2 主窗口左上角显示与任务栏中一样的图标


### 3\.3 状态栏分成两列，还要显示文字


## 4\.使用wxSmith修改sTetris实现与xTetris一致的视觉效果5\.结束语


