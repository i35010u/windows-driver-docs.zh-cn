---
title: RCDRKD 扩展
description: 本部分介绍 RCDRKD 调试器扩展命令。 这些命令将显示创建的驱动程序 WPP 跟踪消息。
ms.assetid: 11CEBCED-2C11-4450-A5FB-BC5B48B1E1A3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6586529095d871411cba84d7fd35667477399182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374803"
---
# <a name="rcdrkd-extensions"></a>RCDRKD 扩展


本部分介绍 RCDRKD 调试器扩展命令。 这些命令将显示创建的驱动程序 WPP 跟踪消息。 从 Windows 8 开始，不再需要单独的跟踪消息格式化 (TMF) 文件以分析 WPP 消息。 TMF 信息存储在正则符号文件 （PDB 文件）。

从 Windows 10 开始，可以使用内核模式和用户模式驱动程序[即时跟踪记录器 (IFR) 的日志中记录跟踪](https://msdn.microsoft.com/library/windows/hardware/dn914610)。 内核模式驱动程序可以使用 RCDRKD 命令以从循环缓冲区中读取消息、 格式化消息，以及在调试器中显示的消息。

**请注意**  不能使用 RCDRKD 命令来查看 UMDF 驱动程序日志、 UMDF 框架日志和 KMDF 框架日志。 若要查看这些日志，请使用[Windows 驱动程序框架扩展 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)命令。

 

Rcdrkd.dll 中实现 RCDRKD 调试器扩展命令。 若要加载的 RCDRKD 命令，请输入 **.load rcdrkd.dll**在调试器中。

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

[ **！ Rcdrkd.rcdrhelp** ](-rcdrkd-rcdrhelp.md)在调试器中显示 RCDRKD 命令的帮助。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPP 软件跟踪](https://go.microsoft.com/fwlink/p?LinkID=251984)

[使用框架的事件记录器](https://go.microsoft.com/fwlink/p?LinkID=251985)

[USB 3.0 扩展](usb-3-extensions.md)

 

 






