---
title: RCDRKD 扩展
description: 本部分介绍 RCDRKD 调试器扩展命令。 这些命令显示驱动程序创建的 WPP 跟踪消息。
ms.assetid: 11CEBCED-2C11-4450-A5FB-BC5B48B1E1A3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df26d9961bf1d0e969d95adc2372efa7519a1143
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534312"
---
# <a name="rcdrkd-extensions"></a>RCDRKD 扩展


本部分介绍 RCDRKD 调试器扩展命令。 这些命令显示驱动程序创建的 WPP 跟踪消息。 从 Windows 8 开始，不再需要单独的跟踪消息格式（TMF）文件来分析 WPP 消息。 TMF 信息存储在常规符号文件（PDB 文件）中。

从 Windows 10 开始，内核模式和用户模式驱动程序可以将[即时 Trace 录像机（IFR）用于日志记录跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)。 内核模式驱动程序可以使用 RCDRKD 命令从循环缓冲区读取消息、设置消息格式，以及在调试器中显示消息。

**注意**   不能使用 RCDRKD 命令来查看 UMDF 驱动程序日志、UMDF framework 日志和 KMDF framework 日志。 若要查看这些日志，请使用[Windows 驱动程序框架扩展（Wdfkd）](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)命令。

 

RCDRKD 调试器扩展命令是在 Rcdrkd 中实现的。 若要加载 RCDRKD 命令，请在调试器中输入**RCDRKD** 。

以下两个命令是用于显示跟踪消息的主要命令。

-   [**!rcdrkd.rcdrlogdump**](-rcdrkd-rcdrlogdump.md)
-   [**!rcdrkd.rcdrcrashdump**](-rcdrkd-rcdrcrashdump.md)

以下辅助命令提供与显示和保存跟踪消息相关的服务。

-   [**!rcdrkd.rcdrloglist**](-rcdrkd-rcdrloglist.md)
-   [**!rcdrkd.rcdrlogsave**](-rcdrkd-rcdrlogsave.md)
-   [**!rcdrkd.rcdrsearchpath**](-rcdrkd-rcdrsearchpath.md)
-   [**!rcdrkd.rcdrsettraceprefix**](-rcdrkd-rcdrsettraceprefix.md)
-   [**!rcdrkd.rcdrtmffile**](-rcdrkd-rcdrtmffile.md)
-   [**!rcdrkd.rcdrtraceprtdebug**](-rcdrkd-rcdrtraceprtdebug.md)

[**！ Rcdrkd rcdrhelp**](-rcdrkd-rcdrhelp.md)在调试器中显示 rcdrkd 命令的帮助。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[使用框架的事件记录器](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-s-event-logger)

[USB 3.0 扩展](usb-3-extensions.md)

 

 






