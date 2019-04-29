---
title: 时光穿越调试 - 示例应用演练
description: 本部分包含一个较小的演练操作C++应用程序。
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6e6156cc4ca85c58dfc909d3494d1df61a934a22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364837"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

#  <a name="time-travel-debugging---sample-app-walkthrough"></a>时光穿越调试 - 示例应用演练

此实验室中引入了时间旅行调试 (TTD)，使用小型示例程序和代码缺陷。 TTD 用于调试、识别问题及分析其根本原因。 虽然很容易地找到此小程序中的问题，可以在更复杂的代码使用常规过程。 此常规步骤可以总结如下。

1. 捕获失败的程序的旅行时间跟踪。
2. 使用[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)命令查找存储在录制中的异常事件。 
3. 使用[！ tt （时程）](time-travel-debugging-extension-tt.md)命令前往的异常事件的跟踪中的位置。
4. 从跟踪单个步骤，直到有问题的错误代码向后在该点进入作用域。
5. 作用域中的错误代码，查看本地值和开发一个假设，可能包含不正确的值的变量。
6. 确定具有不正确的值的变量的内存地址。
7. 在使用 ba 可疑变量的地址上设置内存访问 (ba) 断点[（访问在遇到时中断）](ba--break-on-access-.md)命令。
8. 使用 g-若要运行备份到的可疑的变量的内存访问的最后一个点。
9. 请参阅该位置中或几条指令之前，是否是代码缺陷的点。 如果是这样，你已完成。
如果不正确的值来自于另一个变量，在访问第二个变量上设置断点上设置另一个中断。 
10. 使用 g-返回到最后一个内存访问点上运行第二个可疑的变量。 请参阅该位置或之前的几条指令包含的代码缺陷。 如果是这样，你已完成。
11. 重复此过程的每个步骤直到设置不正确的值导致了错误代码的。
 
在此过程中所述的常规技术将应用于一系列代码问题，尽管存在一些需要一种独特方法的唯一代码问题。 本演练中所示的技术应能扩展已调试的工具集，并将演示一些使用 TTD 跟踪。


## <a name="span-idlabobjectivesspanspan-idlabobjectivesspanspan-idlabobjectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>实验室目的

完成此实验后，你将能够使用与时间旅行跟踪的一般过程来确定代码中的问题。 


## <a name="span-idlabsetupspanspan-idlabsetupspanspan-idlabsetupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>实验室设置

你将需要以下硬件以便能够完成实验室。

-   便携式计算机或台式计算机 （主机） 运行 Windows 10 

你将需要以下软件才能将无法完成该实验。

-   在 WinDbg 预览。 有关安装 WinDbg 预览版的信息，请参阅[WinDbg 预览版的安装](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)
-   若要生成示例的 visual StudioC++代码。 

实验室有以下三个部分。

-   [第 1 部分：生成的示例代码](#build)
-   [第 2 部分：记录跟踪"DisplayGreeting"示例](#record)
-   [第 3 部分：分析跟踪文件记录来标识的代码问题](#analyze)


## <a name="span-idbuildspansection-1-build-the-sample-code"></a><span id="build"></span>第 1 部分：生成的示例代码

*在第 1 部分，将生成使用 Visual Studio 的示例代码。*

**在 Visual Studio 中创建示例应用**

1.  在 Microsoft Visual Studio 中，单击**文件** &gt; **新建** &gt; **项目/解决方案...** ，然后单击视觉对象**C++** 模板。 
    
    选择 Win32 控制台应用程序。

    提供的项目名称*DisplayGreeting* ，然后单击**确定**。

2. 取消选中的安全开发生命周期 (SDL) 检查。

    ![win32 应用程序向导应用程序设置](images/ttd-time-travel-walkthrough-application-wizard-application-settings.png) 

3. 单击**完成**。

3. 粘贴到 Visual Studio 中的 DisplayGreeting.cpp 窗格的以下文本。

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

4.  在 Visual Studio 中，单击**项目** &gt; **DisplayGreeting 属性**。 然后单击**C /C++** 并**代码生成**。

    设置以下属性。

    | 设置              |  ReplTest1                        |
    |----------------------|-------------------------------|
    | 安全检查       | 禁用安全检查 (/ GS-) |
    | 基本运行时检查 |  默认                      |

 
   > [!NOTE]
   > 尽管不建议使用这些设置，很可能很难想象有人会建议使用这些设置，以加快编码，或者为了促进某些测试环境的方案。
   >  

5.  在 Visual Studio 中，单击**构建** &gt; **生成解决方案**。

    如果一切顺利，生成 windows 应显示一条指示成功生成消息。

6.  **查找生成的示例应用文件**

    在解决方案资源管理器，右键单击*DisplayGreeting*项目，然后选择**在文件资源管理器中打开文件夹**。
    
    导航到包含示例的已编译的 exe 和符号 pdb 文件的调试文件夹。 例如，你可以导航到*C:\Projects\DisplayGreeting\Debug*，如果这是在存储你的项目的文件夹。 

7. **运行带有代码缺陷的示例应用**

    双击要运行示例应用程序的 exe 文件。

    ![出错的应用程序对话框](images/ttd-time-travel-walkthrough-faulting-app-dialog-box.png) 

    如果出现此对话框中，选择**关闭程序**

    ![出错的应用程序对话框](images/ttd-time-travel-walkthrough-program-not-working-dialog-box.png) 
    
    在本演练的下一步部分中，我们将记录执行该示例应用以查看是否我们可以确定发生此异常的原因。 


## <a name="span-idrecordspansection-2-record-a-trace-of-the-displaygreeting-sample"></a><span id="record"></span>第 2 部分：记录跟踪"DisplayGreeting"示例

*在第 2 部分，您将记录表现不正常应用程序示例"DisplayGreeting"跟踪*

若要启动示例应用程序和记录 TTD 跟踪，请执行以下步骤。 有关记录 TTD 跟踪的常规信息，请参阅[时间旅行调试-跟踪记录](time-travel-debugging-record.md)

1. 作为管理员，为了使读者到前所未有的速度运行的 WinDbg 预览传输跟踪。

2. 在 WinDbg 预览中，选择**文件** > **开始调试** > **启动可执行文件 （高级）**。

3. 输入你想要记录或选择的用户模式下可执行文件的路径**浏览**以导航到可执行文件。 有关使用启动可执行文件预览的菜单中的 WinDbg 的信息，请参阅[WinDbg 预览版-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示开始录制中的复选框的 WinDbg 预览的屏幕截图启动可执行文件 （高级） 的屏幕](images/ttd-time-travel-walkthrough-recording-app.png)

4. 检查**记录时间旅行调试过程**框来记录跟踪启动可执行文件时。 

5. 单击**确定**启动可执行文件并开始录制。 

6. 记录对话框会显示指示正在记录跟踪。 片刻之后，即，应用程序崩溃。

7. 单击**重试**、 允许尝试并运行的代码。

8. 此程序发生故障，跟踪文件将关闭并写出到磁盘。 

    ![使用索引的 1/1 关键帧中显示输出的 WinDbg 预览的屏幕截图](images/ttd-time-travel-walkthrough-windbg-indexed-frames.png)

9. 调试器将自动打开跟踪文件和其编制索引。 索引是启用的跟踪文件的高效调试的进程。 此索引的过程将需要更长时间，较大的跟踪文件。

    ```dbgcmd
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 95ms.
    ```
   
   > [!NOTE]
   > 关键帧是用于编制索引的跟踪中的位置。 自动生成的关键帧。 更大的跟踪将包含多个关键帧。 
   >   
 
10. 现在您有跟踪文件的开头，并且可以向前和向后时间。

    现在，你已有记录 TTD 跟踪，可以重播跟踪备份或使用跟踪文件，例如其与同事共享。 有关使用跟踪文件的详细信息，请参阅[时间旅行调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)

在本实验的下一部分中我们将分析跟踪文件以查找与我们的代码问题。


## <a name="span-idanalyzespansection-3-analyze-the-trace-file-recording-to-identify-the-code-issue"></a><span id="analyze"></span>第 3 部分：分析跟踪文件记录来标识的代码问题

*在第 3 部分，您将分析跟踪文件记录来标识的代码问题。*

**配置 WinDbg 环境**

1.  将你的本地符号位置添加到符号路径，并通过键入以下命令来重新加载符号。

    ```dbgcmd
    .sympath+ C:\Projects\DisplayGreeting\Debug
    .reload 
    ```

2.  通过键入以下命令将你的本地代码位置添加到源路径。

    ```dbgcmd
    .srcpath C:\Projects\DisplayGreeting\DisplayGreeting
    ```

3. 若要能够查看堆栈和局部变量的状态在 WinDbg 预览功能区上，选择**视图**和**局部变量**并**视图**和**堆栈**. 组织 windows 才能使您可以在同一时间查看、 源代码和命令窗口。

4.  在 WinDbg 预览功能区中，选择**源**并**打开源文件**。 找到 DisplayGreeting.cpp 文件并将其打开。

**检查异常**

1. 已加载的跟踪文件会显示发生了异常的信息。 

    ```dbgcmd
    2fa8.1fdc): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68ef8100 ebx=00000000 ecx=77a266ac edx=69614afc esi=6961137c edi=004da000
    eip=77a266ac esp=0023f9b4 ebp=0023fc04 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:0023fac0=00000000
    ```
2. 使用 dx 命令以列出所有记录中的事件。 异常事件的事件中列出。

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events
    ...
    [0x2c]           : Module Loaded at position: 9967:0
    [0x2d]           : Exception at 9BDC:0
    [0x2e]           : Thread terminated at 9C43:0
    ...
    
    ```

   > [!NOTE]
   > 在本演练中三个句点用于指示已删除无关的输出。 
   >


3. 单击要显示有关该 TTD 事件的信息的异常事件。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17]
    @$curprocess.TTD.Events[17]                 : Exception at 68:0
        Type             : Exception
        Position         : 68:0 [Time Travel]
        Exception        : Exception of type Hardware at PC: 0X540020
    ```


4. 单击进一步向下钻到例外字段下的异常数据。 

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

   异常数据指示这是引发的 CPU 的硬件故障。 它还提供 0xc0000005，该值指示这是访问冲突的异常代码。 这通常表示我们已尝试将写入我们不能访问的内存。

5. 单击要将移动到该位置在跟踪中的异常事件中的 [时程] 链接。

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
    
    请注意，在此输出是堆栈和基指针指向两个非常不同的地址。

    ```dbgcmd
    esp=00effe4c ebp=00520055
    ```

    这可能表示的堆栈损坏-可能是一个函数返回，则损坏堆栈。 若要验证这一点，我们需要出差回之前的 CPU 的状态已损坏，请参阅是否我们可以确定堆栈损坏发生的时间。


**检查本地变量并设置代码断点**

在跟踪中的失败时它是通用的最终 fews 步骤后的错误处理代码中的真正原因。 与时间旅行我们可以返回一次一个指令，以找到调查，则返回 true 的根本原因。


1. 从**主页**功能区使用**到后退**命令来单步后三个指令。 执行此操作时，会持续检查堆栈和内存窗口。

    命令窗口会显示时间旅行位置和寄存器在逐步返回三条指令。

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
   > 在此演练中，命令输出显示了可以使用而不是 UI 菜单选项以允许用户使用命令行使用首选项，若要使用命令行命令的命令。
   > 

2. 此时在跟踪中我们的堆栈和基指针具有更有意义，因此，我们必须在代码中获取更接近于点发生损坏，它显示的值。

    ```dbgcmd
    esp=00effd94 ebp=00effe44
    ```

    此外感兴趣的是代码的，局部变量窗口包含我们的目标应用程序中的值和源代码窗口突出显示的已准备好在跟踪中的此位置执行行。

    ![屏幕截图的 WinDbg 预览显示局部变量窗口与内存的 ASCII 输出和源的代码窗口](images/ttd-time-travel-walkthrough-locals-window.png)

3. 若要进一步调查，我们可以打开一个内存窗口，若要查看的内容的基指针内存地址附近*0x00effe44*。

4. 若要显示的相关联的 ASCII 字符，从内存功能区中，选择**文本**，然后**ASCII**。

    ![winbbg 预览显示内存 ascii 输出和源的代码窗口的屏幕截图](images/ttd-time-travel-walkthrough-memory-ascii.png)

5. 而不指向一个指令的基指针指向我们的消息文本。 因此内容并不就在这里，这可能是接近我们破坏堆栈的时间点。 若要进一步调查，我们将把一个断点。 


> [!NOTE]
> 在本例中很小，它将是一种非常简单，就是在代码中，找到，但如果有数百行代码和几十个子例程可以使用此处所述的技术来减少找到问题所需的时间。
>


**TTD 和断点**

使用断点是暂停的一些事件感兴趣的代码执行的常见方法。  TTD，可设置断点，并返回旅行前的时间中命中断点后已记录跟踪。 后一个问题发生，以确定最佳位置断点，检查进程状态的功能启用唯一的 TTD 其他调试工作流。 

**内存访问断点**

您可以设置触发访问的内存位置时的断点。 使用**ba** （换行的访问权限） 命令，使用以下语法。

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
<th align="left">Option</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>执行 （时 CPU 会从地址中提取一条指令）</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>读/写 （时 CPU 读取或写入到的地址）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>写入 （当 CPU 将写入地址）</p></td>
</tr>
</tbody>
</table>

 
请注意，在任何给定时间只能设置四个数据断点，它将由您来确保将正确对齐数据或将不会触发该断点 （字必须以整除的地址结尾的一半，dword 值必须是整除 4和四字的 0 或 8)。


**设置内存访问断点处中断的基指针**    

1.  此时在跟踪中我们想要对基指针的 ebp 它在我们的示例中为 00effe44 写入内存访问上设置断点。 为此，请使用**ba**命令使用我们想要监视的地址。 我们想要监视写入，四个字节，因此我们指定 w4。 

    ```dbgcmd
    0:000> ba w4 00effe44
    ```

2. 选择**视图**，然后**断点**以确认它们按预期方式设置。

    ![WinDbg 预览显示断点窗口与一个断点](images/ttd-time-travel-walkthrough-view-breakpoints.png)


3.  从主页菜单中选择**转到后退**若要在过去，直到命中断点。

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

4. 选择**视图**，然后**局部变量**。 在局部变量窗口中我们可以看到*目标*变量具有仅消息的一部分，而*源*已包含的所有文本。 此信息支持堆栈已损坏的想法。 

    ![WinDbg 预览屏幕截图局部变量窗口](images/ttd-time-travel-walkthrough-locals-window.png)


5. 现在我们可以检查程序堆栈，以查看哪些代码处于活动状态。 从**视图**功能区选择**堆栈**。 

    ![屏幕截图的 WinDbg 预览堆栈窗口](images/ttd-time-travel-walkthrough-stack-window.png)


由于它是 Microsoft 提供 wscpy_s() 函数将具有一个类似的代码错误不太可能，我们进一步在堆栈中。 堆栈显示问候 ！ 主要调用问候语 ！GetCppConGreeting。 我们非常小的代码示例中我们可以只需在这里打开的代码，并可能非常方便地找到错误。 但是，为了说明可以在更大、 更复杂的程序的技术，我们将设置新断点，以做进一步调查。 


**访问断点处也能 GetCppConGreeting 函数设置中断**        

1. 使用断点窗口通过右键单击现有断点并选择清除现有断点**删除**。

2. 确定 DisplayGreeting 的地址 ！函数使用 DetermineStringSize **dx**命令。 

    ```dbgcmd
    0:000> dx &DisplayGreeting!GetCppConGreeting
    &DisplayGreeting!GetCppConGreeting                 : 0xb61720 [Type: void (__cdecl*)(wchar_t *,unsigned int)]
        [Type: void __cdecl(wchar_t *,unsigned int)]
    ```

3. 使用**ba**内存访问上设置断点的命令。 因为该函数只需将从内存执行读取，我们需要设置 r-读取断点。

    ```dbgcmd
    0:000> ba r4 b61720
    ```

4. 确认在断点窗口中的硬件读取断点处于活动状态。

    ![使用一个硬件 WinDbg 预览显示断点窗口读取断点](images/ttd-time-travel-walkthrough-hardware-write-breakpoint.png)


5. 因为我们想知道有关问候语字符串的大小，我们将把监视窗口将显示 sizeof(greeting) 的值。 从视图功能区中，选择**Watch** ，并提供*sizeof(greeting)*。

    ![WinDbg 预览显示监视局部变量窗口](images/ttd-time-travel-watch-locals.png)

6. 在时间旅行菜单上，使用**按照时间顺序逐个启动**命令将移动到跟踪的开始。

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

7.  在主页菜单中，选择**转**向前移动在代码中直到命中断点。

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


8.  在主页菜单中，选择**单步出后退**到后一个步骤。

    ```dbgcmd
    0:000> g-u
    Time Travel Position: 4B:1AA
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61917 esp=00ddf7ac ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!main+0x27:
    00b61917 e8def7ffff      call    DisplayGreeting!ILT+245(?GetCppConGreetingYAXPA_WIZ) (00b610fa)
    ```


9. 看起来，我们发现根本原因。 *问候*我们声明的数组是长度为 50 个字符，而我们将传递到 GetCppConGreeting sizeof(greeting) 是 0x64，100)。  

    ![显示显示问候语代码与监视局部变量窗口显示 X64 的 WinDbg 预览](images/ttd-time-travel-walkthrough-code-with-watch-locals.png)

    因为我们看一下进一步大小问题，我们还注意到该消息是 76 包括结束字符串字符长度为 75 个字符。

    ```dbgcmd
    HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!
    ```


10. 若要修复此代码的一种方法是扩展到 100 之间的字符数组的大小。

    ```cpp
    std::array <wchar_t, 100> greeting{};
    ```

    并且我们还需要更改 sizeof(greeting) 为 size(greeting) 这行代码中。

    ```cpp
     GetCppConGreeting(greeting.data(), size(greeting));
    ```

11. 若要验证这些修补程序，我们可以重新编译代码，并确认它在运行时没有出错。


**设置断点，使用源窗口**


1. 若要执行此调查的替代方法是通过单击任意代码行上设置断点。 例如在源窗口中的 std:array 定义行右侧单击将存在设置一个断点。

    ![显示在 std:array 上设置断点的源窗口的屏幕截图](images/ttd-time-travel-walkthrough-source-window-breakpoint.png)

2. 在时间旅行菜单上，使用**按照时间顺序逐个启动**命令将移动到跟踪的开始。

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

3. 在主页功能区上单击**转**传输直到命中断点。

    ```dbgcmd
    Breakpoint 0 hit
    Time Travel Position: 5B:AF
    eax=0000000f ebx=00c20000 ecx=00000000 edx=00000000 esi=013a1046 edi=00effa60
    eip=013a17c1 esp=00eff970 ebp=00effa60 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DisplayGreeting+0x41:
    013a17c1 8bf4            mov     esi,esp
    ```


**访问断点上设置中断*问候*变量**    

是另一个替代方法来执行此调查可疑的变量上设置断点并检查哪些代码更改它们。 例如，若要 GetCppConGreeting 方法中的问候语变量上设置断点，使用此过程。

本演练的本部分假定您仍位于上一节中的断点。 

1. 从**视图**，然后**局部变量**。 在局部变量窗口中，*问候*是在当前上下文中可用，因此我们将能够确定其内存位置。 

2.  使用**dx**命令来检查*问候*数组。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    此跟踪中*问候*位于 ddf800 在内存中。 


2. 使用断点窗口中右键单击现有断点并选择通过清除任何现有断点**删除**。


3.  设置的断点**ba**命令使用我们想要监视以进行写访问的内存地址。 

    ```dbgcmd
    ba w4 ddf800
    ```

4. 在时间旅行菜单上，使用**按照时间顺序逐个启动**命令将移动到跟踪的开始。

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

5. 在主页菜单中，选择**转**向前前往问候语数组的内存访问的第一个点。 

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

   或者，我们可以具有为跟踪行程并按相反的顺序浏览代码以查找跟踪中的最后一点数组内存位置写入到的工作。
      

**使用 TTD。若要查看内存访问的内存对象**    

确定在跟踪中的哪些位置访问内存，另一种方法是使用 TTD。内存对象和 dx 命令。

1.  使用**dx**命令来检查*问候*数组。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    此跟踪中*问候*位于 ddf800 在内存中。 

2. 使用**dx**命令，查看从读写访问权限与该地址处开始的内存中的四个字节。

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

3. 单击任何匹配项以显示有关该匹配项的内存访问的详细信息。

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

4. 单击 [时程] 若要跟踪的点位置的时间。

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

5. 如果我们感兴趣的读/写内存访问，则在跟踪中的最后一个匹配项我们可以单击列表中的最后一项或追加。Last （） 函数到 dx 命令的末尾。

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

6. 然后，我们可以 [时程] 若要将移动到该位置在跟踪中单击，并深入介绍代码执行在该位置中，使用之前在此实验室中所述的技术。

有关 TTD 的详细信息。内存对象，请参阅[TTD。内存对象](time-travel-debugging-object-model.md)。


**摘要**      

在本例中很小问题可能已确定通过查看几行代码，但较大的程序在此处介绍的技术可用于减少找到问题所需的时间。 

后记录跟踪时，可以共享的跟踪和重现步骤，并将任何 PC 上按需可重现此问题。  


---

## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

[调试-记录按时间顺序查看](time-travel-debugging-record.md)

[时间旅行调试-重播的跟踪](time-travel-debugging-replay.md)

[调试-使用跟踪文件按时间顺序查看](time-travel-debugging-trace-file-information.md)

---






