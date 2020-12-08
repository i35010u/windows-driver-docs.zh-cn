---
title: RCDRKD 扩展
description: 本部分介绍 RCDRKD 调试器扩展命令。 这些命令显示驱动程序创建的 WPP 跟踪消息。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 336cd5c175c1e38d5ec4494742b7f11209425947
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839795"
---
# <a name="rcdrkd-extensions"></a>RCDRKD 扩展


本部分介绍 RCDRKD 调试器扩展命令。 这些命令显示驱动程序创建的 WPP 跟踪消息。 从 Windows 8 开始，不再需要单独的跟踪消息格式 (TMF) 文件来分析 WPP 消息。 TMF 信息存储在 (PDB 文件) 的常规符号文件中。

从 Windows 10 开始，内核模式和用户模式驱动程序可以使用 [即时 Trace 录像机 (IFR) 进行日志记录跟踪](../devtest/using-wpp-recorder.md)。 内核模式驱动程序可以使用 RCDRKD 命令从循环缓冲区读取消息、设置消息格式，以及在调试器中显示消息。

**注意**  不能使用 RCDRKD 命令来查看 UMDF 驱动程序日志、UMDF framework 日志和 KMDF framework 日志。 若要查看这些日志，请使用 [Windows 驱动程序框架扩展 ( # A0) ](kernel-mode-driver-framework-extensions--wdfkd-dll-.md) 命令。

 

RCDRKD 调试器扩展命令在 Rcdrkd.dll 中实现。 若要加载 RCDRKD 命令，请输入调试程序中的 **load rcdrkd.dll** 。

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


[WPP 软件跟踪](../devtest/wpp-software-tracing.md)

[使用框架的事件记录器](../wdf/using-the-framework-s-event-logger.md)

[USB 3.0 扩展](usb-3-extensions.md)

 

