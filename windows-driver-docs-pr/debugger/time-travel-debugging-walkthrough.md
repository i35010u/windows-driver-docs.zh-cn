---
title: 时光穿越调试 - 示例应用演练
description: 本部分包含一个小型C++应用程序的演练。
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9799911fdfcfeedb507df63ac8de8cd39458b360
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916146"
---
# <a name="time-travel-debugging---sample-app-walkthrough"></a>时光穿越调试 - 示例应用演练

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

此实验室使用带有代码缺陷的小型示例程序引入了时间行程调试（TTD）。 TTD 用于调试、识别问题及分析其根本原因。 尽管此小程序中的问题易于查找，但可以在更复杂的代码上使用常规过程。 可按如下所示总结此常规过程。

1. 捕获失败的程序的时间行程跟踪。
2. 使用 " [dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md) " 命令可查找存储在记录中的异常事件。 
3. 使用[！ tt （时间段）](time-travel-debugging-extension-tt.md)命令可以在跟踪中移动到异常事件的位置。
4. 从跟踪中的那一步开始向后翻一步，直到所述的错误代码进入范围为止。
5. 使用范围内出错的代码，查看本地值并开发可能包含错误值的变量假设。
6. 确定具有错误值的变量的内存地址。
7. 使用 "ba [（访问时中断）](ba--break-on-access-.md) " 命令在可疑变量地址上设置内存访问（ba）断点。
8. 使用 g-返回到可疑变量的最后一个内存访问点。
9. 查看此位置，或前面的说明是否是代码缺陷的点。 如果是这样，就大功告成了。
如果不正确的值来自其他某个变量，请在第二个变量的访问断点处设置另一个分行符。 
10. 使用 g-返回到第二个置疑变量上的最后一个内存访问点。 在包含代码缺陷之前，请查看该位置或一些说明。 如果是这样，就大功告成了。
11. 重复此过程，直到设置了导致错误的错误值的代码。
 
尽管本过程中介绍的常规技术适用于一系列广泛的代码问题，但有一些唯一的代码问题需要唯一的方法。 本演练中所述的技术应提供扩展调试工具集的功能，并说明 TTD 跟踪可能会发生的一些情况。


## <a name="span-idlab_objectivesspanspan-idlab_objectivesspanspan-idlab_objectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>实验室目标

完成此实验后，您将能够使用带有时间行程跟踪的常规过程来找出代码中的问题。 


## <a name="span-idlab_setupspanspan-idlab_setupspanspan-idlab_setupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>实验室设置

你将需要以下硬件才能完成实验室。

-   运行 Windows 10 的便携式计算机或台式计算机（主机） 

你将需要以下软件才能完成实验室。

-   WinDbg 预览。 有关安装 WinDbg Preview 的信息，请参阅[WinDbg 预览版-安装](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)
-   Visual Studio 生成示例C++代码。 

实验室包含以下三个部分。

-   [第1节：生成示例代码](#build)
-   [第2部分：记录 "DisplayGreeting" 示例的跟踪](#record)
-   [第3部分：分析跟踪文件记录以确定代码问题](#analyze)


## <a name="span-idbuildspansection-1-build-the-sample-code"></a><span id="build"></span>第1节：生成示例代码

*在第1部分中，你将使用 Visual Studio 生成示例代码。*

**在 Visual Studio 中创建示例应用**

1.  在 Microsoft Visual Studio 中，单击 "**文件**" &gt;**新建**&gt;**项目/解决方案 ...** "，然后单击**C++** 视觉对象模板。 
    
    选择 "Win32 控制台应用程序"。

    提供项目名称 " *DisplayGreeting* "，并单击 **"确定"** 。

2. 取消选中 "安全开发生命周期（SDL）检查"。

    ![win32 应用程序向导应用程序设置](images/ttd-time-travel-walkthrough-application-wizard-application-settings.png) 

3. 单击 "**完成**"。

3. 将以下文本粘贴到 Visual Studio 中的 DisplayGreeting 窗格。

    ```cpp
    // DisplayGreeting.cpp : Defines the entry point for the console application.
    //

    #include "stdafx.h"
    #include <array>
    #include <stdio.h>
    #include <string.h>

    void GetCppConGreeting(wchar_t* buffer, size_t size)
    {
       wchar_t const* const message = L"HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!";
 
       wcscpy_s(buffer, size, message);
    }

    int main()
    {
        std::array <wchar_t, 50> greeting{};
        GetCppConGreeting(greeting.data(), sizeof(greeting));

        wprintf(L"%ls\n", greeting.data());

        return 0;
    }
    ```

4.  在 Visual Studio 中，单击 "**项目**&gt; **DisplayGreeting" 属性**"。 然后单击 " **C/C++**  " 和 "**代码生成**"。

    设置以下属性。

    | 设置              |  Value                        |
    |----------------------|-------------------------------|
    | 安全检查       | 禁用安全检查（/GS-） |
    | 基本运行时检查 |  Default                      |

 
   > [!NOTE]
   > 尽管不建议使用这些设置，但也可以想象出这样一种情况：有人建议使用这些设置来加速编码或促进某些测试环境。
   >  

5.  在 Visual Studio 中，单击 "**生成**&gt;**生成解决方案**"。

    如果一切顺利，生成窗口应显示一条消息，指示生成已成功。

6.  **找到生成的示例应用文件**

    在解决方案资源管理器中，右键单击*DisplayGreeting*项目，然后选择 "**在文件资源管理器中打开文件夹**"。
    
    导航到包含该示例的编译后的 exe 和符号 pdb 文件的 Debug 文件夹。 例如，如果您的项目存储在*C:\Projects\DisplayGreeting\Debug*中，则可以导航到该文件夹。 

7. **运行具有代码缺陷的示例应用程序**

    双击 exe 文件以运行示例应用。

    !["错误应用" 对话框](images/ttd-time-travel-walkthrough-faulting-app-dialog-box.png) 

    如果出现此对话框，请选择 "**关闭程序**"

    !["错误应用" 对话框](images/ttd-time-travel-walkthrough-program-not-working-dialog-box.png) 
    
    在本演练的下一部分中，我们将记录示例应用程序的执行情况，以确定是否可以确定发生此异常的原因。 


## <a name="span-idrecordspansection-2-record-a-trace-of-the-displaygreeting-sample"></a><span id="record"></span>第2部分：记录 "DisplayGreeting" 示例的跟踪

*在第2部分中，你将记录 "DisplayGreeting" 应用程序的行为*

若要启动示例应用并录制 TTD 跟踪，请执行以下步骤。 有关记录 TTD 跟踪的常规信息，请参阅[行程调试-录制跟踪](time-travel-debugging-record.md)

1. 以管理员身份运行 WinDbg Preview，以便能够记录时间行程跟踪。

2. 在 WinDbg Preview 中，选择 "**文件**" > **启动调试** > **启动可执行文件（高级）** 。

3. 输入要记录的用户模式可执行文件的路径，或选择 "**浏览**" 以导航到可执行文件。 有关使用 WinDbg Preview 中的 "启动可执行文件" 菜单的信息，请参阅[Windbg preview-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示 "启动可执行（高级）" 屏幕上的 "开始记录" 复选框的 WinDbg 预览屏幕截图](images/ttd-time-travel-walkthrough-recording-app.png)

4. 使用 "**时间段调试**" 框检查记录过程，以便在启动可执行文件时记录跟踪。 

5. 单击 **"确定"** 以启动可执行文件并开始记录。 

6. 此时将显示 "记录" 对话框，指示正在记录跟踪。 不久之后，应用程序就会崩溃。

7. 单击 "**重试**" 以允许代码尝试并运行。

8. 程序崩溃，跟踪文件将关闭并写出到磁盘。 

    ![显示带1/1 关键帧索引输出的 WinDbg 预览的屏幕截图](images/ttd-time-travel-walkthrough-windbg-indexed-frames.png)

9. 调试器将自动打开并为跟踪文件编制索引。 索引是一种能够有效调试跟踪文件的过程。 对于较大的跟踪文件，此索引过程需要更长的时间。

    ```dbgcmd
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 95ms.
    ```
   
   > [!NOTE]
   > 关键帧是跟踪中用于索引的位置。 自动生成关键帧。 较大的跟踪将包含更多关键帧。 
   >   
 
10. 此时，你处于跟踪文件的开头，并且已准备好向前和向后移动。

    现在已经记录了 TTD 跟踪，你可以重播该跟踪或使用跟踪文件，例如，将其与同事共享。 有关使用跟踪文件的详细信息，请参阅[行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)

在此实验的下一部分中，我们将分析跟踪文件，以找出我们的代码问题。


## <a name="span-idanalyzespansection-3-analyze-the-trace-file-recording-to-identify-the-code-issue"></a><span id="analyze"></span>第3部分：分析跟踪文件记录以确定代码问题

*在第3部分中，您将分析跟踪文件记录以确定代码问题。*

**配置 WinDbg 环境**

1.  键入以下命令，将本地符号位置添加到符号路径中，并重新加载符号。

    ```dbgcmd
    .sympath+ C:\Projects\DisplayGreeting\Debug
    .reload 
    ```

2.  键入以下命令，将本地代码位置添加到源路径。

    ```dbgcmd
    .srcpath C:\Projects\DisplayGreeting\DisplayGreeting
    ```

3. 若要能够查看堆栈和局部变量的状态，请在 WinDbg 预览功能区中选择 "**视图**" 和 "**局部变量**" 和 "**视图**和**堆栈**"。 组织窗口，使您可以同时查看它们、源代码和命令窗口。

4.  在 WinDbg 预览功能区中，选择 "**源文件**" 和 "**打开源文件**"。 找到并打开 DisplayGreeting 文件。

**检查异常**

1. 加载跟踪文件后，它会显示发生异常的信息。 

    ```dbgcmd
    2fa8.1fdc): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68ef8100 ebx=00000000 ecx=77a266ac edx=69614afc esi=6961137c edi=004da000
    eip=77a266ac esp=0023f9b4 ebp=0023fc04 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:0023fac0=00000000
    ```
2. 使用 dx 命令列出记录中的所有事件。 事件中列出了 exception 事件。

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events
    ...
    [0x2c]           : Module Loaded at position: 9967:0
    [0x2d]           : Exception at 9BDC:0
    [0x2e]           : Thread terminated at 9C43:0
    ...
    
    ```

   > [!NOTE]
   > 在本演练中，三个期间用于指示已移除无关的输出。 
   >


3. 单击 "异常" 事件以显示有关该 TTD 事件的信息。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17]
    @$curprocess.TTD.Events[17]                 : Exception at 68:0
        Type             : Exception
        Position         : 68:0 [Time Travel]
        Exception        : Exception of type Hardware at PC: 0X540020
    ```


4. 单击 "异常" 字段，进一步向下钻取异常数据。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17].Exception
    @$curprocess.TTD.Events[17].Exception                 : Exception of type Hardware at PC: 0X540020
        Position         : 68:0 [Time Travel]
        Type             : Hardware
        ProgramCounter   : 0x540020
        Code             : 0xc0000005
        Flags            : 0x0
        RecordAddress    : 0x0
    ```

   异常数据指示这是 CPU 引发的硬件故障。 它还提供了0xc0000005 的异常代码，指示这是一个访问冲突。 这通常表示我们尝试写入无法访问的内存。

5. 在异常事件中单击 [Time 旅行] 链接，以移动到跟踪中的该位置。

    ```dbgcmd
    0:000> dx @$curprocess.TTD.Events[17].Exception.Position.SeekTo()
    Setting position: 68:0

    @$curprocess.TTD.Events[17].Exception.Position.SeekTo()
    (16c8.1f28): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 68:0
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00540020 esp=00effe4c ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    00540020 ??              
    ```
    
    注意，在此输出中，堆栈和基指针指向两个不同的地址。

    ```dbgcmd
    esp=00effe4c ebp=00520055
    ```

    这可能表示堆栈损坏，可能是因为函数返回，然后损坏堆栈。 若要对此进行验证，需要在 CPU 状态损坏之前返回到，并查看是否可以确定发生堆栈损坏的时间。


**检查局部变量并设置代码断点**

跟踪失败时，通常会在错误处理代码的真正原因后最终 fews 的步骤。 使用时间段，我们可以一次返回一条指令，查找真正的根本原因。


1. 从 "**主页**" 功能区中，使用 "**单步**执行" 命令返回三个指令。 执行此操作时，请继续检查堆栈和内存窗口。

    当你逐步执行三个说明时，"命令" 窗口会显示时间。

    ```dbgcmd
    0:000> t-
    Time Travel Position: 67:40
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00540020 esp=00effe4c ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    00540020 ??              ???

    0:000> t-
    Time Travel Position: 67:3F
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=0019193d esp=00effe48 ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    DisplayGreeting!main+0x4d:
    0019193d c3    

    0:000> t-
    Time Travel Position: 67:39
    eax=0000004c ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00191935 esp=00effd94 ebp=00effe44 iopl=0         nv up ei pl nz ac po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000212
    DisplayGreeting!main+0x45:
    ```

   > [!NOTE]
   > 在本演练中，命令输出显示可用于代替 UI 菜单选项的命令，以允许具有命令行使用首选项的用户使用命令行命令。
   > 

2. 此时，在跟踪中，堆栈和基指针的值会更有意义，因此，我们似乎已更接近发生损坏的代码中的点。

    ```dbgcmd
    esp=00effd94 ebp=00effe44
    ```

    还需要注意的是，"局部变量" 窗口包含来自目标应用的值，并且 "源代码" 窗口突出显示了已准备好在跟踪中执行的代码行。

    ![WinDbg 预览的屏幕截图，显示具有内存 ASCII 输出和源代码窗口的局部变量窗口](images/ttd-time-travel-walkthrough-locals-window.png)

3. 若要进一步调查，可以打开 "内存" 窗口，查看*0x00effe44*的基本指针内存地址附近的内容。

4. 若要显示关联的 ASCII 字符，请在 "内存" 功能区中选择 "**文本**"，然后选择 " **ASCII**"。

    ![显示 "内存 ascii 输出和源代码" 窗口的 winbbg 预览屏幕截图](images/ttd-time-travel-walkthrough-memory-ascii.png)

5. 它不是指向说明消息文本的基指针。 这里不是这样，这可能接近于损坏堆栈的时间点。 若要进一步调查，请设置一个断点。 


> [!NOTE]
> 在这个非常小的示例中，只需查看代码，就可以很容易地查找代码，但如果有数百行代码和几十个子例程，则可以使用此处所述的技术来缩短查找问题所需的时间。
>


**TTD 和断点**

使用断点是一种在相关事件中暂停代码执行的常见方法。  使用 TTD 可以设置断点，并在记录跟踪后，在该断点到达之前进行回退。 在出现问题后检查进程状态的功能，若要确定断点的最佳位置，可以启用 TTD 独有的其他调试工作流。 

**内存访问断点**

可以设置在访问内存位置时激发的断点。 使用以下语法，使用 " **ba** （访问时中断）" 命令。

```dbgcmd
ba <access> <size> <address> {options}
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>电邮</p></td>
<td align="left"><p>execute （当 CPU 从地址提取指令时）</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>读/写（CPU 读取或写入地址时）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>水平</p></td>
<td align="left"><p>写入（CPU 写入地址时）</p></td>
</tr>
</tbody>
</table>

 
请注意，在任何给定时间，只能设置四个数据断点，并由您确保正确对齐数据或不触发断点（单词必须以2为界限的地址结束，dword 必须可被4整除），并按0或 8 quadwords）。


**设置基指针的内存访问断点中断**    

1.  此时，我们要在跟踪中设置一个断点，使其在对基指针-ebp 的访问上进行设置，在本例中为00effe44。 若要执行此操作，请使用 " **ba** " 命令，使用我们要监视的地址。 我们想要监视四个字节的写入，因此我们指定 w4。 

    ```dbgcmd
    0:000> ba w4 00effe44
    ```

2. 选择 "**查看**"，然后选择 "**断点**" 以确认它们按预期设置。

    ![WinDbg 预览显示带有一个断点的 "断点" 窗口](images/ttd-time-travel-walkthrough-view-breakpoints.png)


3.  在 "主文件夹" 中 **，选择 "返回到**后一次"，直到命中断点。

    ```dbgcmd
    0:000> g-
    Breakpoint 0 hit
    Time Travel Position: 5B:92
    eax=0000000f ebx=003db000 ecx=00000000 edx=00cc1a6c esi=00d41046 edi=0053fde8
    eip=00d4174a esp=0053fcf8 ebp=0053fde8 iopl=0         nv up ei pl nz ac pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000216
    DisplayGreeting!DisplayGreeting+0x3a:
    00d4174a c745e000000000  mov     dword ptr [ebp-20h],0 ss:002b:0053fdc8=cccccccc
    ```

4. 选择 "**视图**"，然后选择 "**局部变量**"。 在 "局部变量" 窗口中，可以看到*目标*变量只包含消息的一部分，而*源*包含所有文本。 此信息支持堆栈损坏。 

    ![WinDbg 预览 "局部变量" 窗口的屏幕截图](images/ttd-time-travel-walkthrough-locals-window.png)


5. 此时，我们可以检查程序堆栈以查看哪些代码处于活动状态。 从 "**视图**" 功能区中选择 "**堆栈**"。 

    ![WinDbg 预览堆栈窗口的屏幕截图](images/ttd-time-travel-walkthrough-stack-window.png)


由于 Microsoft 提供的 wscpy_s （）函数不太可能出现类似于下面的代码 bug，因此我们将在堆栈中进一步进行查找。 此堆栈显示问候语！ main 拨打问候语！GetCppConGreeting. 在我们非常小的代码示例中，现在可以打开代码，这可能会非常容易地发现错误。 但为了阐释可用于更大、更复杂的程序的技术，我们将设置一个新的断点以进行进一步调查。 


**设置 GetCppConGreeting 函数的访问断点中断**        

1. 使用 "断点" 窗口通过右键单击现有断点并选择 "**删除**" 来清除现有断点。

2. 确定 DisplayGreeting 的地址！DetermineStringSize 函数。 

    ```dbgcmd
    0:000> dx &DisplayGreeting!GetCppConGreeting
    &DisplayGreeting!GetCppConGreeting                 : 0xb61720 [Type: void (__cdecl*)(wchar_t *,unsigned int)]
        [Type: void __cdecl(wchar_t *,unsigned int)]
    ```

3. 使用**ba**命令设置内存访问上的断点。 由于只需从内存中读取函数以便执行，因此需要设置 r 读取断点。

    ```dbgcmd
    0:000> ba r4 b61720
    ```

4. 确认 "断点" 窗口中的 "硬件读取" 断点处于活动状态。

    ![WinDbg 预览显示带有一个硬件读取断点的 "断点" 窗口](images/ttd-time-travel-walkthrough-hardware-write-breakpoint.png)


5. 当我们想知道问候语字符串的大小时，我们将设置一个 "监视" 窗口来显示 "sizeof" （问候语）的值。 从 "视图" 功能区中，选择 "**观看**并提供*sizeof （问候语）* "。

    ![显示 "监视局部变量" 窗口的 WinDbg 预览](images/ttd-time-travel-watch-locals.png)

6. 在 "时间段" 菜单中，使用 "**时间段启动**" 命令移动到跟踪开始处。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

7.  在主菜单上，选择 "**转**到" 以在代码中向前移动，直到命中断点。

    ```dbgcmd
    0:000> g
    Breakpoint 2 hit
    Time Travel Position: 4B:1AD
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61721 esp=00ddf7a4 ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!GetCppConGreeting+0x1:
    00b61721 8bec            mov     ebp,esp
    ```


8.  在 "主文件夹" 菜单上，选择 "**跳出**一步"。

    ```dbgcmd
    0:000> g-u
    Time Travel Position: 4B:1AA
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61917 esp=00ddf7ac ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!main+0x27:
    00b61917 e8def7ffff      call    DisplayGreeting!ILT+245(?GetCppConGreetingYAXPA_WIZ) (00b610fa)
    ```


9. 这似乎是我们找到根本原因。 我们声明的*问候语*数组的长度为50个字符，而传入 GetCppConGreeting 的 sizeof （问候）为0x64，100）。  

    ![WinDbg 预览版显示显示问候语代码，并显示 "监视" "局部变量" 窗口显示 X64](images/ttd-time-travel-walkthrough-code-with-watch-locals.png)

    当我们进一步查看大小问题时，我们还会注意到，消息长度为75个字符76，其中包括字符串的末尾。

    ```dbgcmd
    HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!
    ```


10. 修复代码的一种方法是将字符数组的大小扩展为100。

    ```cpp
    std::array <wchar_t, 100> greeting{};
    ```

    还需要在此代码行中将 sizeof （问候）改为大小（问候）。

    ```cpp
     GetCppConGreeting(greeting.data(), size(greeting));
    ```

11. 若要验证这些修复程序，我们可以重新编译代码并确认它运行不会出错。


**使用源窗口设置断点**


1. 执行此调查的另一种方法是通过单击任意代码行来设置断点。 例如，单击 "源" 窗口中 "std： array" 定义行的右侧将设置一个断点。

    ![显示 std： array 上设置的断点的源窗口的屏幕截图](images/ttd-time-travel-walkthrough-source-window-breakpoint.png)

2. 在 "时间段" 菜单中，使用 "**时间段启动**" 命令移动到跟踪开始处。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

3. 在 "主页" 功能区上，单击 "**前往**"，直至命中断点。

    ```dbgcmd
    Breakpoint 0 hit
    Time Travel Position: 5B:AF
    eax=0000000f ebx=00c20000 ecx=00000000 edx=00000000 esi=013a1046 edi=00effa60
    eip=013a17c1 esp=00eff970 ebp=00effa60 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DisplayGreeting+0x41:
    013a17c1 8bf4            mov     esi,esp
    ```


**为*问候语*变量设置访问断点中断**    

执行此调查的另一种方法是，在置疑变量上设置断点，并检查哪些代码正在更改它们。 例如，若要在 GetCppConGreeting 方法中的问候语变量上设置一个断点，请使用此过程。

本部分演练假设你仍位于上一部分的断点处。 

1. 从 "**视图**" 和 "**局部变量**"。 在 "局部变量" 窗口中，*问候*在当前上下文中可用，因此，我们将能够确定其内存位置。 

2.  使用**dx**命令检查*问候语*数组。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    在此跟踪中，*问候语*位于 ddf800 的内存中。 


2. 使用 "断点" 窗口可以通过右键单击现有断点并选择 "**删除**" 来清除任何现有断点。


3.  使用用于监视写入访问的内存地址的**ba**命令设置断点。 

    ```dbgcmd
    ba w4 ddf800
    ```

4. 在 "时间段" 菜单中，使用 "**时间段启动**" 命令移动到跟踪开始处。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

5. 在 "主文件夹" 菜单上，选择 "**转**到"，使其前进到问候语数组的第一个内存访问点。 

    ```dbgcmd
    0:000> g-
    Breakpoint 0 hit
    Time Travel Position: 5B:9C
    eax=cccccccc ebx=002b1000 ecx=00000000 edx=68d51a6c esi=013a1046 edi=001bf7d8
    eip=013a1735 esp=001bf6b8 ebp=001bf7d8 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DetermineStringSize+0x25:
    013a1735 c745ec04000000  mov     dword ptr [ebp-14h],4 ss:002b:001bf7c4=cccccccc
    ```

   另外，我们还可以将旅行到跟踪的末尾，并在代码中反向工作，以查找已写入数组内存位置的跟踪中的最后一个点。
      

**请使用 TTD。用于查看内存访问的内存对象**    

确定跟踪内存中的哪些点被访问的另一种方法是使用 TTD。内存对象和 dx 命令。

1.  使用**dx**命令检查*问候语*数组。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    在此跟踪中，*问候语*位于 ddf800 的内存中。 

2. 使用**dx**命令查看内存中以 "读写访问" 开头的四个字节。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")
    @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
        [0x4]           
        [0x5]           
        [0x6]           
        [0x7]           
        [0x8]           
        [0x9]           
        [0xa]           
        ...         
    ```

3. 单击任一匹配项以显示有关该内存访问发生情况的详细信息。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5]
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5]                
        EventType        : MemoryAccess
        ThreadId         : 0x710
        UniqueThreadId   : 0x2
        TimeStart        : 27:3C1 [Time Travel]
        TimeEnd          : 27:3C1 [Time Travel]
        AccessType       : Write
        IP               : 0x6900432f
        Address          : 0xddf800
        Size             : 0x4
        Value            : 0xddf818
    ```

4. 单击 "时间段" 以在时间点放置跟踪。

    ```dbgcmd
    0:000> dx @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5].TimeStart.SeekTo()
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5].TimeStart.SeekTo()
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 27:3C1
    eax=00ddf81c ebx=00fa2000 ecx=00ddf818 edx=ffffffff esi=00000000 edi=00b61046
    eip=6900432f esp=00ddf804 ebp=00ddf810 iopl=0         nv up ei pl nz ac po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000212
    ucrtbased!_register_onexit_function+0xf:
    6900432f 51              push    ecx
   ```

5. 如果对跟踪中最后一次出现的读取/写入内存访问感兴趣，可以单击列表中的最后一项或追加。Last （）函数到 dx 命令的结尾。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw").Last()
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw").Last()                
        EventType        : MemoryAccess
        ThreadId         : 0x710
        UniqueThreadId   : 0x2
        TimeStart        : 53:100E [Time Travel]
        TimeEnd          : 53:100E [Time Travel]
        AccessType       : Read
        IP               : 0x690338e4
        Address          : 0xddf802
        Size             : 0x2
        Value            : 0x45
    ```

6. 然后，可以单击 [Time 旅行]，在跟踪中移动到该位置，并使用本实验室中前面所述的技术进一步查看代码执行。

有关 TTD 的详细信息。内存对象，请参阅[TTD。内存对象](time-travel-debugging-object-model.md)。

**摘要**  

在这个非常小的示例中，此问题可能是通过查看几行代码来确定的，但是在大型程序中，此处提供的方法可用于缩短查找问题所需的时间。 

记录跟踪后，可以共享跟踪和重现步骤，并且在任何电脑上，此问题都可以按需重现。  

---

## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)

[旅行调试-记录](time-travel-debugging-record.md)

[旅行调试-重播跟踪](time-travel-debugging-replay.md)

[时间行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)
