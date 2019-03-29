---
title: 使用 Logger.exe
description: 使用 Logger.exe
ms.assetid: da2ec999-4529-49dc-855e-a7d3b15583f7
keywords:
- 记录器、 logger.exe
- logger.exe
- 记录器独立
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc67028c19a1575721470d7f438981a64b890978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576094"
---
# <a name="using-loggerexe"></a>使用 Logger.exe


## <span id="ddk_using_logger_exe_dtoolq"></span><span id="DDK_USING_LOGGER_EXE_DTOOLQ"></span>


若要激活记录器的一种方法是运行独立 Logger.exe 程序。 这是实质上是一个只能采用单个目标的非常小的调试器。 若要运行它，包括命令行上的目标应用程序的名称：

```dbgcmd
logger Target 
```

这激活时，它将加载指定的应用程序，并将代码插入到加载并初始化 Logexts.dll 目标应用程序进程中的例程中将跳转关闭目标应用程序。 这被称为"到目标应用程序注入记录器"。

Logger.exe 实用工具和 Logexts.dll 模块是此记录器车辆的两个组件。 它们通过共享包含输出文件句柄、 当前类别掩码和指向日志输出缓冲区的指针的内存的一部分进行通信。

标题为一个窗口**记录器 （调试器）** 将出现。 此窗口将显示记录器的进度。

### <a name="span-idchangesettingsdialogboxspanspan-idchangesettingsdialogboxspanchange-settings-dialog-box"></a><span id="change_settings_dialog_box"></span><span id="CHANGE_SETTINGS_DIALOG_BOX"></span>更改设置对话框

初始化完成并且初始显示已完成后,**更改设置**对话框将出现。 这允许你配置记录器设置。 此处所述的各种设置：

<span id="API_Settings"></span><span id="api_settings"></span><span id="API_SETTINGS"></span>**API 设置**  
此列表显示可用的 API 类别。 突出显示的类别将记入日志;将不会将非突出显示的类别。 首次运行记录器，所有类别将突出都显示。 但是，在后续运行中，记录器将跟踪的给定的目标应用程序选择的类别。

如果禁用某个类别，则将删除该类别中的所有 Api 的挂钩，以便不再对性能产生影响。 COM 挂钩不会删除，因为它们不能随意重新启用。

您只是想特定类型的程序具有与 Windows-例如，文件操作的交互时，允许仅特定类别可能会有用。 这可以减少日志文件大小，而且还可以减少的记录器进程的执行速度上产生的影响。

<span id="Logging"></span><span id="logging"></span><span id="LOGGING"></span>**日志记录**  
本部分包含**启用**并**禁用**单选按钮。 禁用日志记录将导致所有 API 挂钩，为了允许自由地运行应用程序中删除。 COM 挂钩不会删除，因为它们不能随意重新启用。

<span id="Inclusion___Exclusion_List"></span><span id="inclusion___exclusion_list"></span><span id="INCLUSION___EXCLUSION_LIST"></span>**包含 / 排除列表**  
此部分控制模块包含/排除列表。 通常是需要日志从一个特定模块或一组模块进行这些函数调用。 若要使这更为简便，记录器，可指定模块包含列表，或者模块排除列表。 例如，如果只想将记录从一个或两个模块的调用将使用包含列表。 如果您想要日志从一个模块的简短列表除外的所有模块进行的调用，则会使用排除列表。 始终排除 Logexts.dll 和 Kernel32.dll 的模块，因为不允许使用记录器以记录本身。

<span id="Flush_the_Buffer"></span><span id="flush_the_buffer"></span><span id="FLUSH_THE_BUFFER"></span>**刷新缓冲区**  
此按钮将刷新的当前输出缓冲区。 作为性能的考虑因素，日志输出被刷新到磁盘仅当输出缓冲区已满时。 默认情况下，缓冲区为 2144 字节。

因为缓冲区内存由目标应用程序，如果发生访问冲突或某些其他不可恢复的错误目标应用程序中不会发生自动写入到磁盘上的日志文件的缓冲区。 在这种情况下，应尝试激活目标应用程序的窗口并按 F12 获取回来，此对话框，然后按**刷新缓冲区**。 如果不执行此操作，最近记录函数可能不会出现在日志文件中。

<span id="Go"></span><span id="go"></span><span id="GO"></span>**转到**  
这将导致目标应用程序开始执行。

### <a name="span-idrunningthetargetapplicationspanspan-idrunningthetargetapplicationspanrunning-the-target-application"></a><span id="running_the_target_application"></span><span id="RUNNING_THE_TARGET_APPLICATION"></span>运行目标应用程序

一旦选择了设置后，单击**转**。 对话框将关闭，并且目标应用程序将开始运行。

如果您使目标应用程序的窗口处于活动状态，并按 F12，它将中断到记录器。 这将导致要冻结的目标应用程序和**更改设置**对话框再次出现。 您可以更改设置，如果您愿意，，然后按**转**继续执行。

可以根据需要为运行目标应用程序。 通常情况下或因出错而终止它，如果日志记录将停止，并且不能重新启动。

当你想要退出时，则选择**文件 |退出**然后单击**是**。 如果目标应用程序仍在运行，则会终止。

### <a name="span-idlimitationsofloggerexespanspan-idlimitationsofloggerexespanlimitations-of-loggerexe"></a><span id="limitations_of_logger_exe"></span><span id="LIMITATIONS_OF_LOGGER_EXE"></span>Logger.exe 的限制

当通过 Logger.exe 工具正在运行记录器时，它将创建只有一个输出文件--.lgv 文件。 没有文本文件将被写入。 但是，将创建大小为零的.txt 文件;这可能会覆盖以前由调试器编写的文本日志。

输出文件将始终放置在桌面上; LogExts 子目录中不能更改此位置。

如果通过调试器和 Logexts.dll 运行记录器，不会应用这些限制。

 

 





