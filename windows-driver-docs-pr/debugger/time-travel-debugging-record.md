---
title: 旅行调试-记录跟踪
description: 本部分介绍如何记录时间行程跟踪。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd00b081d108c7473c70dd63e7ef88a52d1d8d5a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916168"
---
#  <a name="time-travel-debugging---record-a-trace"></a>旅行调试-记录跟踪 

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

本部分介绍如何记录时间行程调试（TTD）跟踪。 可以通过两种方法在 WinDbg Preview 中记录跟踪，*启动可执行文件（高级）* 并*附加到进程*。 

## <a name="launch-executable-advanced"></a>启动可执行文件（高级）

若要启动可执行文件并记录 TTD 跟踪，请执行以下步骤。

1. 在 WinDbg Preview 中，选择 "**文件**" > **启动调试** > **启动可执行文件（高级）** 。

2. 输入要记录的用户模式可执行文件的路径，或选择 "**浏览**" 以导航到可执行文件。 有关使用 WinDbg Preview 中的 "启动可执行文件" 菜单的信息，请参阅[Windbg preview-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示 "启动可执行（高级）" 屏幕上的 "开始记录" 复选框的 WinDbg 预览屏幕截图](images/ttd-start-recording.png)


3. 使用 "**时间段调试**" 框检查记录过程，以便在启动可执行文件时记录跟踪。 

4. 单击 **"确定"** 以启动可执行文件并开始记录。 

5. 此时将显示 "记录" 对话框，指示正在记录跟踪。

    ![显示停止和调试以及取消选项的 TTD 录制弹出窗口](images/ttd-recording-pop-up.png)

6. 有关记录的信息，请参阅[如何记录](#HOWTORECORD)。


## <a name="attach-to-a-process"></a>附加到进程

若要附加到进程并记录 TTD 跟踪，请执行以下步骤。

1. 在 WinDbg Preview 中，选择 "**文件**" > "**开始调试**" > **附加到进程**"。

2. 选择要跟踪的用户模式进程。 有关在 WinDbg Preview 中使用 "*附加到进程*" 菜单的详细信息，请参阅[Windbg preview-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示 "开始记录" 复选框的 WinDbg 预览屏幕截图](images/ttd-start-recording-attach-to-process.png)


3. 使用 "**时间段调试**" 框检查记录过程，以便在启动可执行文件时创建跟踪。 

4. 单击 "**附加**" 开始录制。 

5. 此时将显示 "记录" 对话框，指示正在记录跟踪。

    ![显示停止和调试以及取消选项的 TTD 录制弹出窗口](images/ttd-recording-pop-up-attach.png)

6. 有关记录的信息，请参阅[如何记录](#HOWTORECORD)。

## <a name="span-idhowtorecordspanspan-idhowtorecordspanhow-to-record"></a><span id="HOWTORECORD"></span><span id="howtorecord"></span>如何录制

1. 正在记录此过程，因此需要引起要调试的问题。 您可以打开有问题的文件，或者单击应用中的某个特定按钮，使发生感兴趣的事件。 

2. 在显示 "录制" 对话框时，可以：

    - **停止和调试**-选择此项将停止记录，创建跟踪文件并打开跟踪文件，以便您可以开始调试。 
    - **取消**-选择此项将停止记录并创建跟踪文件。 稍后可以打开跟踪文件。 
   
3. 录制完成后，请关闭应用或**停止和调试**。

   > [!NOTE]
   > *停止和调试* *都将终止关联的进程*。 
   >   

4. 当记录的应用程序终止时，跟踪文件将关闭并写出到磁盘。 如果程序崩溃，就会出现这种情况。

5. 打开跟踪文件时，调试器将自动为跟踪文件编制索引。 索引可实现更准确、更快的内存价值查找。 对于较大的跟踪文件，此索引过程需要更长的时间。

    ```dbgcmd
    ...
    00007ffc`61f789d4 c3              ret
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 96ms.
    ```
   > [!NOTE]
   > 关键帧是跟踪中用于索引的位置。 自动生成关键帧。 较大的跟踪将包含更多关键帧。 对跟踪进行索引后，将显示关键帧的数量。 
   >   
 
6. 此时，你处于跟踪文件的开头，并且已准备好向前和向后移动。

    > [!TIP]
    > 使用断点是一种在相关事件中暂停代码执行的常见方法。  TTD 是唯一的，你可以设置断点，并在记录跟踪后，在命中该断点之前及时播放。 在出现问题后检查进程状态的功能，确定断点的最佳位置，启用其他调试工作流。 有关过去使用断点的示例，请参阅[行程调试-示例应用演练](time-travel-debugging-walkthrough.md)。

## <a name="next-steps"></a>后续步骤

现在已经记录了 TTD 跟踪，你可以重播该跟踪或使用跟踪文件，例如，将其与同事共享。 有关详细信息，请参阅这些主题。

[旅行调试-重播跟踪](time-travel-debugging-replay.md)

[时间行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)

[行程调试-故障排除](time-travel-debugging-troubleshooting.md)

[旅行调试-示例应用演练](time-travel-debugging-walkthrough.md)

## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)

