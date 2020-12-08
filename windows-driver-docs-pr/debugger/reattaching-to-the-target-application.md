---
title: 重新附加到目标应用程序
description: 重新附加到目标应用程序
keywords:
- 重新附加到目标应用程序
- 处理，将调试器重新连接到
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95cf7c66ce9e91933ac07fbee87397962fac4017
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811201"
---
# <a name="reattaching-to-the-target-application"></a>重新附加到目标应用程序


## <span id="ddk_re_attaching_to_the_target_application_dbg"></span><span id="DDK_RE_ATTACHING_TO_THE_TARGET_APPLICATION_DBG"></span>


如果调试器冻结或停止响应 (即，当你执行用户模式调试时， *崩溃*) ，你可以将新的调试器附加到现有进程。

**注意**  此方法仅在 Microsoft Windows XP 和更高版本的 Windows 上受支持。 此方法并不取决于调试器最初是创建进程还是附加到现有进程。 此方法并不取决于是否使用了 **-pd** 选项。

 

若要将调试器重新连接到现有的目标应用程序，请执行以下操作：

1.  确定目标应用程序的[进程 ID](finding-the-process-id.md) 。

2.  启动 CDB 或 WinDbg 的新实例。 使用 **-pe** 命令行选项。

    ```console
    Debugger -pe -p PID 
    ```

    你还可以使用其他 [命令行选项](command-line-options.md)。

    还可以通过使用 [**. attach (attach To Process)**](-attach--attach-to-process-.md) 命令与 **-e** 选项连接。

3.  附加完成后，结束原始调试器进程。

4.  如果该进程没有正确响应，则可能是挂起计数过高。 可以使用 [**~ m (Resume Thread)**](-m--resume-thread-.md) 命令来减少挂起计数。 有关挂起计数的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

如果原始调试器仍然运行正常，则此方法可能不起作用。 这两个调试器争用调试事件，Windows 操作系统不一定将所有调试事件分配给新调试器。

如果在附加新调试器之前结束了原始调试器，则目标应用程序也会关闭。  (但是，如果调试器附加了 **-pd** 选项，然后正常退出，则目标应用程序将继续运行。 在这种情况下，第二个调试器可以附加到目标应用程序，而无需使用 **-pe** 选项。 ) 

如果你已在调试进程，并且想要从进程中分离，但使其冻结在调试状态，则可以使用 [**. (放弃进程)**](-abandon--abandon-process-.md) 命令。 完成此命令后，任何 Windows 调试器都可以通过使用本主题中所述的过程重新附加到该进程。

 

 





