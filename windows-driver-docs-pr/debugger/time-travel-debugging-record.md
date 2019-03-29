---
title: 时间旅行调试-记录跟踪
description: 本部分介绍如何记录时间旅行跟踪。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e14b0493deab84b02f55d646e1f91511b687b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568515"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

#  <a name="time-travel-debugging---record-a-trace"></a>时间旅行调试-记录跟踪 

本部分介绍如何记录时间顺序查看调试 (TTD) 跟踪。 有两种方法以在 WinDbg 预览版中，记录跟踪*启动可执行文件 （高级）* 并*附加到进程*。 


## <a name="launch-executable-advanced"></a>启动可执行文件 （高级）

若要启动可执行文件和记录 TTD 跟踪，请执行以下步骤。

1. 在 WinDbg 预览中，选择**文件** > **开始调试** > **启动可执行文件 （高级）**。

2. 输入你想要记录或选择的用户模式下可执行文件的路径**浏览**以导航到可执行文件。 有关使用 WinDbg 预览版中的启动可执行文件菜单的信息，请参阅[WinDbg 预览版-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示开始录制中的复选框的 WinDbg 预览的屏幕截图启动可执行文件 （高级） 的屏幕](images/ttd-start-recording.png)


3. 检查**记录时间旅行调试过程**框来记录跟踪启动可执行文件时。 

4. 单击**确定**启动可执行文件并开始录制。 

5. 记录对话框会显示指示正在记录跟踪。

    ![TTD 录制弹出窗口显示停止和调试也一样取消选项](images/ttd-recording-pop-up.png)

6. 请参阅[记录](#HOWTORECORD)有关记录的信息。


## <a name="attach-to-a-process"></a>附加到进程

若要附加到进程和记录 TTD 跟踪，请执行以下步骤。

1. 在 WinDbg 预览中，选择**文件** > **开始调试** > **附加到进程**。

2. 选择想要跟踪的用户模式进程。 有关使用信息*附加到进程*WinDbg 预览菜单中的看到[WinDbg 预览版-启动用户模式会话](windbg-user-mode-preview.md)。

    ![显示开始录制复选框的 WinDbg 预览的屏幕截图](images/ttd-start-recording-attach-to-process.png)


3. 检查**时间旅行调试记录过程**框，以启动可执行文件时创建跟踪。 

4. 单击**附加**开始录制。 

5. 记录对话框会显示指示正在记录跟踪。

    ![TTD 录制弹出窗口显示停止和调试也一样取消选项](images/ttd-recording-pop-up-attach.png)

6. 请参阅[记录](#HOWTORECORD)有关记录的信息。

## <a name="span-idhowtorecordspanspan-idhowtorecordspanhow-to-record"></a><span id="HOWTORECORD"></span><span id="howtorecord"></span>如何记录

1. 过程将被记录，因此，这是您需要会导致你想要调试的问题。 可能打开文件有问题，或单击特定按钮中应用，使要发生的事件。 

2. 当显示记录对话框中，你可以：

    - **停止和调试**-选择这将停止录制，创建跟踪文件并打开跟踪文件，因此您可以开始调试。 
    - **取消**-选择这将停止记录，并创建跟踪文件。 在更高版本时，可以打开跟踪文件。 
   
3. 录制完成后，关闭您的应用程序或命中**停止和调试**。

   > [!NOTE]
   > 这两*停止和调试*并*取消*将终止关联的进程。 
   >   

4. 当正在记录的应用程序终止时，跟踪文件将为已关闭并写出到磁盘。 如果您的程序也崩溃，这是这种情况。

5. 打开跟踪文件时，调试器将自动创建索引的跟踪文件。 索引可更准确、 更快的内存值查找。 此索引的过程将需要更长时间，较大的跟踪文件。

    ```dbgcmd
    ...
    00007ffc`61f789d4 c3              ret
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 96ms.
    ```
   > [!NOTE]
   > 关键帧是用于编制索引的跟踪中的位置。 自动生成的关键帧。 更大的跟踪将包含多个关键帧。 当跟踪进行索引编制时，显示的关键帧数。 
   >   
 
6. 现在您有跟踪文件的开头，并且可以向前和向后时间。

    > [!TIP]
    > 使用断点是暂停的一些事件感兴趣的代码执行的常见方法。  唯一 TTD，您可以设置断点并在过去，直到已记录跟踪后，将命中该断点。 后一个问题发生，以确定最佳位置断点，检查进程状态的功能使其他调试工作流。 在过去使用断点的示例，请参阅[时间旅行调试-示例应用程序演练](time-travel-debugging-walkthrough.md)。

## <a name="next-steps"></a>后续步骤

现在，你已有记录 TTD 跟踪，可以重播跟踪备份或使用跟踪文件，例如其与同事共享。 有关详细信息，请参阅以下主题。

[时间旅行调试-重播的跟踪](time-travel-debugging-replay.md)

[调试-使用跟踪文件按时间顺序查看](time-travel-debugging-trace-file-information.md)

[时间顺序查看调试-故障排除](time-travel-debugging-troubleshooting.md)

[时间旅行调试-示例应用程序演练](time-travel-debugging-walkthrough.md)



## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---






