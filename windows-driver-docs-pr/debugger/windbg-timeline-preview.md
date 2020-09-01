---
title: WinDbg 预览版 - 时间线
description: 本部分介绍如何在 WinDbg Preview 中使用时间段功能。
ms.date: 07/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: cbba3e53942feb67082f09a44862d2f73c4a9b46
ms.sourcegitcommit: cd84cc10570384b0e7a91cb6f91fe67009c1a90e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89238149"
---
# <a name="windbg-preview---timelines"></a>WinDbg 预览版 - 时间线

![带有位模式的 windbg 预览的小徽标](images/windbgx-preview-logo.png)

行程调试 (TTD) 允许用户记录跟踪，这是程序的执行记录。 时间线是执行过程中发生的事件的直观表示形式。 这些事件可以是以下位置：断点、内存读取/写入、函数调用和返回以及异常。

![调试器中显示异常、内存访问、断点和函数调用的时间线](images/windbgx-timeline.png)

使用 "时间线" 窗口可以快速查看重要事件，了解相对位置，并轻松跳到它们在 TTD 跟踪文件中的位置。 使用多个时间线直观地浏览行程跟踪中的事件并发现事件相关。

当打开 TTD 跟踪文件并显示关键事件时，将显示 "时间线" 窗口，无需手动创建数据模型查询。 同时，所有的旅行对象均可用于实现更复杂的数据查询。

有关创建和使用时间行程跟踪文件的详细信息，请参阅 [时间段调试-概述](time-travel-debugging-overview.md)。

## <a name="types-of-timelines"></a>时间线类型

"时间线" 窗口可以显示以下事件：

-  (可以进一步筛选特定异常代码的异常) 
- 添加断点时，还会自动添加断点 (时间线) 
- 函数调用 (按 module！ function 形式搜索) 
- 内存访问 (两个内存地址之间的读取/写入/执行) 

将鼠标悬停在每个事件上，以通过工具提示获取详细信息。 单击某个事件将对该事件运行查询并显示详细信息。 双击某个事件将跳转到 TTD 跟踪文件中的该位置。

### <a name="exceptions"></a>例外

当您加载跟踪文件并且时间线处于活动状态时，它会自动显示记录中的任何异常。

当你将鼠标悬停在断点信息（如异常类型）上时，将显示异常代码。

![调试器中的时间线，显示的异常显示一个异常代码的信息](images/windbgx-timeline-exceptions.png)

您可以使用可选的异常代码字段进一步筛选特定异常代码。

!["时间线调试器异常" 对话框，显示将时间线类型设置为异常，将异常代码设置为0xC0000004](images/windbgx-timeline-exceptions-dialog.png)

还可以为特定异常类型添加新的时间线。

### <a name="breakpoints"></a>断点

添加断点时，将在时间线上自动添加断点时间线。 这可以使用 [最佳实践设置断点命令](bp--bu--bm--set-breakpoint-.md)来实现。 当你将鼠标悬停在断点上方时，将显示与该断点关联的地址和指令指针。

![调试器中的时间线显示大约30个断点点](images/windbgx-timeline-breakpoints.png)

清除断点时，会自动删除关联的断点时间线。

### <a name="function-calls"></a>函数调用

可以在时间线上显示函数调用的位置。 为此，请以的形式提供搜索 `module!function` ，例如 `TimelineTestCode!multiplyTwo` 。 例如，您还可以指定通配符 `TimelineTestCode!m*` 。

![在调试器中添加时间线，并显示类型化的函数调用名称](images/windbgx-timeline-function-calls-dialog.png)

当您将鼠标悬停在函数调用上时，将显示函数名称、输入参数、它们的值和返回值。 此示例显示了 *缓冲区* 和 *大小* ，因为这些是 DisplayGreeting 的参数！GetCppConGreeting.

![调试器中的时间线显示函数调用和寄存器窗口](images/windbgx-timeline-function-calls.png)

### <a name="memory-access"></a>内存访问

使用 "内存访问时间线" 可以在特定范围的内存已读写到或执行代码执行时显示。 开始和停止地址用于定义两个内存地址之间的范围。

![添加 "时间线内存访问" 对话框，其中显示了 "写入" 按钮](images/windbgx-timeline-memory-access-dialog.png)

当你将鼠标悬停在内存访问项上方时，将显示值和指令指针。

![调试器中的时间线显示内存访问](images/windbgx-timeline-memory-access.png)

## <a name="work-with-timelines"></a>使用时间线

当鼠标悬停在时间线上时，它的垂直灰色线条跟随光标。 垂直蓝线指示跟踪中的当前位置。

单击放大镜图标可在时间线上放大和缩小。

在顶部时间线控制区中，使用矩形平移时间线视图。 拖动矩形的外部分隔符以调整当前时间线视图的大小。

![调试器中显示用于选择活动视区的顶部区域的时间线](images/windbgx-timeline-manipulation.png)

### <a name="mouse-movements"></a>鼠标移动

使用 Ctrl + 滚轮放大和缩小。

使用 Shift + 滚轮从一端平移。

## <a name="timeline-debugging-techniques"></a>时间线调试技术

若要演示调试时间线技术，请在此处重复使用 [行程调试演练](time-travel-debugging-walkthrough.md) 。 此演示假定您已完成前两个步骤来生成示例代码并使用前面介绍的前两个步骤创建了 TTD 记录。

[第1节：生成示例代码](./time-travel-debugging-walkthrough.md#build)

[第2部分：记录 "DisplayGreeting" 示例的跟踪](./time-travel-debugging-walkthrough.md#record)

在此方案中，第一步是在行程跟踪中找到异常。 只需要双击时间线上的唯一异常即可完成此操作。

在 "命令" 窗口中，我们看到在单击异常时发出了以下命令。

```dbgcmd
(2dcc.6600): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: CC:0
@$curprocess.TTD.Events.Where(t => t.Type == "Exception")[0x0].Position.SeekTo()
```

选择 "**查看**  >>  **注册**" 可在时间线中的这一点显示收银机，开始调查。

![调试器中显示 demolab 异常和寄存器的时间线](images/windbgx-timeline-demo-lab-exception-registers.png)

在命令输出中，请注意堆栈 (esp) ，而基指针 (ebp) 将指向两个不同的地址。 这可能表示堆栈损坏，可能是因为函数返回，然后损坏堆栈。 若要对此进行验证，需要在 CPU 状态损坏之前返回到，并查看是否可以确定发生堆栈损坏的时间。

正如我们所做的那样，我们将检查局部变量和堆栈的值。

选择 "**查看**  >>  **局部变量**" 以显示本地值。

选择 "**查看**  >>  **堆栈**" 可显示代码执行堆栈。

跟踪失败时，通常会在错误处理代码的真正原因后结束几个步骤。 使用时间段，我们可以一次返回一条指令，找出真正的根本原因。

从 " **主页** " 功能区中，使用 " **单步** 执行" 命令返回三个指令。 执行此操作时，请继续检查堆栈、局部变量和注册窗口。

当你逐步执行三个说明时，"命令" 窗口会显示时间。

```dbgcmd
0:000> t-
Time Travel Position: CB:41
eax=00000000 ebx=00564000 ecx=c0d21d62 edx=7a1e4a6c esi=00061299 edi=00061299
eip=00540020 esp=003cf7d0 ebp=00520055 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
00540020 ??              ???
0:000> t-
Time Travel Position: CB:40
eax=00000000 ebx=00564000 ecx=c0d21d62 edx=7a1e4a6c esi=00061299 edi=00061299
eip=00061767 esp=003cf7cc ebp=00520055 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
DisplayGreeting!main+0x57:
00061767 c3              ret
0:000> t-
Time Travel Position: CB:3A
eax=0000004c ebx=00564000 ecx=c0d21d62 edx=7a1e4a6c esi=00061299 edi=00061299
eip=0006175f esp=003cf718 ebp=003cf7c8 iopl=0         nv up ei pl nz na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
DisplayGreeting!main+0x4f:
0006175f 33c0            xor     eax,eax
```

此时，在跟踪中，堆栈和基指针的值会更有意义，因此，我们似乎已更接近发生损坏的代码中的点。

```dbgcmd
esp=003cf718 ebp=003cf7c8
```

还需要注意的是，"局部变量" 窗口包含来自目标应用的值，并且 "源代码" 窗口突出显示了在跟踪中这一时刻可以在源代码中执行的代码行。

若要进一步调查，可以打开 "内存" 窗口，查看堆栈指针附近的内容 (esp) 内存地址。 在此示例中，它的值为003cf7c8。 选择 "**内存**  >>  **文本**  >>  **ASCII** " 以显示在该地址存储的 ASCII 文本。

![显示寄存器堆栈和内存窗口的调试器](images/windbgx-timeline-demo-lab-registers-stack-memory.png)

## <a name="memory-access-timeline"></a>内存访问时间线

确定了感兴趣的内存位置之后，使用该值添加内存访问时间线。 单击 " **+ 添加时间线** "，并填写起始地址。 我们将查看4个字节，因此，将其添加到003cf7c8 的起始地址，我们已003cf7cb。 默认情况下，将查看所有内存写入，但你也可以查看该地址上的写入或代码执行。

![添加一个时间线内存访问对话框，其中显示了 "写入" 按钮，并显示了003cf7c8 的起始值](images/windbgx-timeline-demo-lab-memory-access-dialog.png)

现在，我们可以反向遍历时间线以检查此时间段内的旅行跟踪写入此内存位置的时间。 在时间线中单击此位置时，会看到局部变量值不同于要复制的字符串的值。 目标值显示为 "不完整"，因为字符串的长度不正确。

![内存访问时间线和 "局部变量" 窗口，其中显示源和目标的具有不同值的局部变量值](images/windbgx-timeline-demo-lab-memory-access.png)

## <a name="breakpoint-timeline"></a>断点时间线

使用断点是一种在相关事件中暂停代码执行的常见方法。 使用 TTD 可以设置断点，并在记录跟踪后，在该断点到达之前进行回退。 在出现问题后检查进程状态的功能，若要确定断点的最佳位置，可以启用 TTD 独有的其他调试工作流。

若要浏览备用时间线调试方法，请单击时间线中的异常，并再次使用 "**主页**" 功能区上的 "**单步**执行" 命令向后移动三个步骤。  

在这个非常小的示例中，只需查看代码，就可以很容易地查找代码，但如果有数百行代码和几十个子例程，则可以使用此处所述的技术来缩短查找问题所需的时间。

如前文所述，基指针 (esp) ，而不是指向说明，指向我们的消息文本。

使用 ba 命令设置内存访问上的断点。 我们将设置一个 w 写入断点来查看此内存区域的写入时间。

```dbgcmd
0:000> ba w4 003cf7c8
```

尽管我们将使用简单的内存访问断点，但可以将断点构建为更复杂的条件语句。 有关详细信息，请参阅 [最佳实践、bu、bm.exe (设置断点) ](bp--bu--bm--set-breakpoint-.md)。

在 "主文件夹" 中 **，选择 "返回到** 后一次"，直到命中断点。

此时，我们可以检查程序堆栈以查看哪些代码处于活动状态。

![调试器中的时间线，显示内存访问时间线和堆栈窗口](images/windbgx-timeline-demo-lab-stack.png)

由于 Microsoft 提供的 wscpy_s ( # A1 函数不太可能出现类似于下面的代码 bug，因此我们将进一步探讨堆栈。 此堆栈显示问候语！ main 拨打问候语！GetCppConGreeting. 在我们非常小的代码示例中，现在可以打开代码，这可能会非常容易地发现错误。 但为了阐释可用于更大、更复杂的程序的技术，我们将设置 "添加函数调用时间线"。

## <a name="function-call-timeline"></a>函数调用时间线

单击 " **+ 添加时间线** "，并填写 `DisplayGreeting!GetCppConGreeting` 函数搜索字符串的。

"开始位置和结束位置" 复选框指示跟踪中函数调用的开始和结束。

我们可以使用 dx 命令显示函数调用对象，以查看关联的 TimeStart 和 TimeEnd 字段，它们对应于函数调用的起始位置和结束位置。

```dbgcmd
dx @$cursession.TTD.Calls("DisplayGreeting!GetCppConGreeting")[0x0]
    EventType        : 0x0
    ThreadId         : 0x6600
    UniqueThreadId   : 0x2
    TimeStart        : 6D:BD [Time Travel]
    SystemTimeStart  : Thursday, October 31, 2019 23:36:05
    TimeEnd          : 6D:742 [Time Travel]
    SystemTimeEnd    : Thursday, October 31, 2019 23:36:05
    Function         : DisplayGreeting!GetCppConGreeting
    FunctionAddress  : 0x615a0
    ReturnAddress    : 0x61746
    Parameters  
```

必须选中 "开始" 或 "结束" 或 "开始" 和 "结束位置" 框。

![添加新的时间线对话框，显示添加函数调用时间线和函数搜索字符串 DisplayGreeting！GetCppConGreeting](images/windbgx-timeline-demo-lab-function-dialog.png)

由于我们的代码既不是递归的，也不是可重入的，因此在调用 GetCppConGreeting 方法时，可以很容易地在时间行上查找。 对 GetCppConGreeting 的调用还会同时与我们定义的断点和内存访问事件同时出现。 这样，我们就可以很容易地在代码区域中仔细查看应用程序崩溃的根本原因。

![调试器中的时间线，用于显示内存访问时间线和使用带有不同字符串值的消息和缓冲区的本地窗口](images/windbgx-timeline-demo-lab-function.png)

## <a name="explore-code-execution-by-viewing-multiple-timelines"></a>通过查看多个时间线浏览代码执行

虽然我们的代码示例很小，但使用多个时间线的方法允许对时间旅行跟踪进行可视浏览。 您可以查看跟踪文件来询问问题，如 "遇到断点之前何时访问了内存区域？"。

![调试器中显示内存访问时间线和本地窗口的时间线](images/windbgx-timeline-demo-lab-locals.png)

查看其他关联和查找可能不需要的东西的功能，将时间线工具与使用命令行命令与时间跟踪跟踪进行交互。

## <a name="timeline-bookmarks"></a>时间线书签

在 WinDbg 将重要的时间旅行位置做成书签，而不是手动将位置粘贴到记事本。 使用书签，可以更轻松地查看相对于其他事件的跟踪中的不同位置，并为其添加批注。

可以为书签提供描述性名称。

![显示问候语应用中第一个 api 调用的示例名称的 "新建书签" 对话框](images/windbgx-timeline-bookmark-new.png)

通过 *> 时间线视图*中提供的 "时间线" 窗口访问书签。 当您将鼠标悬停在某个书签上方时，它将显示书签名称。

![显示在一个显示书签名称的书签上方的三个书签的时间线](images/windbgx-timeline-bookmarks.png)

您可以右键单击书签以到达该位置，重命名或删除书签。

![书签右键单击显示旅行以定位编辑和删除的弹出菜单](images/windbgx-timeline-bookmark-edit.png)

### <a name="see-also"></a>另请参阅

[使用 WinDbg 预览版进行调试](debugging-using-windbg-preview.md)

[行程调试演练](time-travel-debugging-walkthrough.md)