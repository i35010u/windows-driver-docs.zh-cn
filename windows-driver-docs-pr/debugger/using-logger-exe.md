---
title: 使用 Logger.exe
description: 使用 Logger.exe
ms.assetid: da2ec999-4529-49dc-855e-a7d3b15583f7
keywords:
- 记录器，logger.exe
- logger.exe
- 记录器，独立
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1492794d9fe07e388851f5cba27c02724742e65
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802797"
---
# <a name="using-loggerexe"></a>使用 Logger.exe


## <span id="ddk_using_logger_exe_dtoolq"></span><span id="DDK_USING_LOGGER_EXE_DTOOLQ"></span>


激活记录器的一种方法是运行独立的 Logger.exe 程序。 这实质上是一个非常小的调试程序，只能采用单个目标。 若要运行此命令，请在命令行中包括目标应用程序的名称：

```dbgcmd
logger Target 
```

激活此功能后，它将加载指定的应用程序，并将代码插入目标应用程序，该应用程序将跳转到在目标应用程序进程中加载和初始化 Logexts.dll 的例程。 这称为 "将记录器注入到目标应用程序中"。

Logger.exe 实用工具和 Logexts.dll 模块是此记录器车辆的两个组件。 它们通过内存的共享部分进行通信，其中包括输出文件句柄、当前类别掩码和指向日志输出缓冲区的指针。

将出现标题为 **记录器 (调试器) ** 的窗口。 此窗口将显示记录器的进度。

### <a name="span-idchange_settings_dialog_boxspanspan-idchange_settings_dialog_boxspanchange-settings-dialog-box"></a><span id="change_settings_dialog_box"></span><span id="CHANGE_SETTINGS_DIALOG_BOX"></span>"更改设置" 对话框

初始化完成并且初始显示完成后，将显示 " **更改设置** " 对话框。 这允许你配置记录器设置。 下面介绍了各种设置：

<span id="API_Settings"></span><span id="api_settings"></span><span id="API_SETTINGS"></span>**API 设置**  
此列表显示可用的 API 类别。 将记录突出显示的类别;不突出显示的类别将不会。 首次运行记录器时，将突出显示所有类别。 但是，在后续运行中，记录器将跟踪为给定目标应用程序选择的类别。

如果已禁用某一类别，则将删除该类别中所有 Api 的挂钩，以便不再出现任何性能开销。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

仅当对程序与 Windows 有关的特定类型的交互（例如，文件操作）感兴趣时，才启用特定类别会很有用。 这会减少日志文件的大小，还会减少记录器对进程执行速度产生的影响。

<span id="Logging"></span><span id="logging"></span><span id="LOGGING"></span>**记**  
本部分包含 " **启用** " 和 " **禁用** " 单选按钮。 禁用日志记录将导致删除所有 API 挂钩，以使程序可以自由运行。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

<span id="Inclusion___Exclusion_List"></span><span id="inclusion___exclusion_list"></span><span id="INCLUSION___EXCLUSION_LIST"></span>**包含/排除列表**  
本部分控制模块包含/排除列表。 通常，只需记录从特定模块或模块集发出的函数调用。 为了便于使用，记录器可以指定模块包含列表或模块排除列表。 例如，如果您只想从一个或两个模块记录调用，则应使用包含列表。 如果你想要记录来自所有模块的调用，而不是较短的模块列表，则可以使用排除列表。 始终会排除 Logexts.dll 和 Kernel32.dll 模块，因为记录器不允许记录自身。

<span id="Flush_the_Buffer"></span><span id="flush_the_buffer"></span><span id="FLUSH_THE_BUFFER"></span>**刷新缓冲区**  
此按钮将刷新当前输出缓冲区。 作为性能方面的考虑，仅当输出缓冲区已满时才将日志输出刷新到磁盘。 默认情况下，缓冲区为2144字节。

由于缓冲区内存由目标应用程序管理，因此，如果在目标应用程序中出现访问冲突或其他不可恢复的错误，则不会将缓冲区自动写入磁盘上的日志文件。 在这种情况下，应尝试激活目标应用程序的窗口，然后单击 "F12" 以返回此对话框，然后按 **"刷新" 缓冲区**。 如果未执行此操作，则最新记录的函数可能不会出现在日志文件中。

<span id="Go"></span><span id="go"></span><span id="GO"></span>**至**  
这会导致目标应用程序开始执行。

### <a name="span-idrunning_the_target_applicationspanspan-idrunning_the_target_applicationspanrunning-the-target-application"></a><span id="running_the_target_application"></span><span id="RUNNING_THE_TARGET_APPLICATION"></span>运行目标应用程序

选择设置后，选择 " **开始**"。 该对话框将关闭，目标应用程序将开始运行。

如果使目标应用程序的窗口处于活动状态，并按 F12 键，则会中断记录器。 这将导致目标应用程序冻结，并且 " **更改设置** " 对话框将重新出现。 如果需要，可以更改设置， **然后按 "继续"** 以继续执行。

您可以根据需要让目标应用程序运行。 如果它正常终止或发生错误，则日志记录将停止并且无法重新启动。

如果希望退出，请选择 " **文件" |退出** ，然后选择 **"是"**。 如果目标应用程序仍在运行，则将终止该应用程序。

### <a name="span-idlimitations_of_logger_exespanspan-idlimitations_of_logger_exespanlimitations-of-loggerexe"></a><span id="limitations_of_logger_exe"></span><span id="LIMITATIONS_OF_LOGGER_EXE"></span>Logger.exe 的限制

通过 Logger.exe 工具运行记录器时，它将只创建一个输出文件-lgv 文件。 将不写入任何文本文件。 但是，将创建一个大小为零的 .txt 文件;这可能会覆盖前面调试器写入的文本日志。

输出文件将始终放在桌面的 LogExts 子目录中;此位置不能更改。

如果通过调试器并 Logexts.dll 运行记录器，则将不会应用这些限制。

 

 





