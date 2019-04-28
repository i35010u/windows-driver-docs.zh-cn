---
title: 重新附加到目标应用程序
description: 重新附加到目标应用程序
ms.assetid: cc137185-58a7-44bf-b262-2698c46730f6
keywords:
- 重新附加到目标应用程序
- 过程中，重新附加到调试器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d905d9f297174bb6a6583ee83a2de207806d1b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353604"
---
# <a name="reattaching-to-the-target-application"></a>重新附加到目标应用程序


## <span id="ddk_re_attaching_to_the_target_application_dbg"></span><span id="DDK_RE_ATTACHING_TO_THE_TARGET_APPLICATION_DBG"></span>


如果调试器冻结，或者否则停止响应 (即*崩溃*) 尽管执行用户模式下调试，可以将新的调试器附加到现有进程。

**请注意**  仅在 Microsoft Windows XP 和更高版本的 Windows 上支持此方法。 此方法不依赖于是否在调试器最初创建进程或附加到现有进程。 此方法不依赖于是否使用 **-pd**选项。

 

若要将调试器重新连接到现有的目标应用程序，执行以下步骤：

1.  [确定进程 ID](finding-the-process-id.md)的目标应用程序。

2.  启动 CDB 或 WinDbg 的新实例。 使用 **-pe**命令行选项。

    ```console
    Debugger -pe -p PID 
    ```

    您还可以使用其他[命令行选项](command-line-options.md)。

    此外可以通过使用连接从休眠调试器[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)命令一起 **-e**选项。

3.  附加完成后，最终原始调试器进程。

4.  如果未正确响应过程，它可能具有挂起计数过高。 可以使用[ **~ （恢复线程） 的 m** ](-m--resume-thread-.md)命令，以减少挂起计数。 有关详细信息计数时挂起，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

如果原始调试器仍能正常运行，此方法可能无法工作。 两个调试器在争夺调试事件和 Windows 操作系统不一定分配的所有调试事件到新的调试器。

如果原始调试器结束之前附加新的调试器，同时关闭目标应用程序。 (但是，如果使用附加调试器 **-pd**选项，然后退出，通常情况下，目标应用程序继续运行。 在此情况下，第二个调试器可以附加到目标应用程序而无需使用 **-pe**选项。)

如果你已调试的进程并想要从过程但保留它冻结处于调试状态，可以使用分离[ **.abandon （放弃进程）** ](-abandon--abandon-process-.md)命令。 此命令后任何 Windows 调试器可以附加到该进程使用本主题中所述的过程。

 

 





