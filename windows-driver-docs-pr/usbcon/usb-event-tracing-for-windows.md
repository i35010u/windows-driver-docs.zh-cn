---
description: 本主题提供有关适用于通用串行总线 (USB) 的跟踪和日志记录功能的客户端驱动程序开发人员的信息。
title: Windows 的 USB 事件跟踪的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c31bec02de9157fe75315132d8bac8253d39c63
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969234"
---
# <a name="overview-of-usb-event-tracing-for-windows"></a>Windows 的 USB 事件跟踪的概述


本主题提供有关适用于通用串行总线 (USB) 的跟踪和日志记录功能的客户端驱动程序开发人员的信息。 提供此信息是为了帮助开发和调试 USB 设备的用户。 它包括有关如何安装这些工具、创建跟踪文件和分析 USB 跟踪文件中的事件的信息。 本主题假定你全面了解了成功使用 USB 跟踪和日志记录功能所需的 USB 生态系统和硬件。

若要解释事件跟踪，还必须了解 [windows 中的 Windows USB 主机端驱动程序](usb-3-0-driver-stack-architecture.md)、 [官方 USB 规范和 USB 设备类规范](https://www.usb.org/documents)。

-   [关于 Windows 事件跟踪](#about-event-tracing-for-windows)
-   [支持 ETW 日志记录的 USB](#usb-support-for-etw-logging)
-   [Windows 7 中的 USB ETW 支持](#usb-etw-support-in-windows-7)
-   [Windows 8 中的 USB ETW 支持](#usb-etw-support-in-windows-8)

## <a name="about-event-tracing-for-windows"></a>关于 Windows 事件跟踪


Windows (ETW) 的事件跟踪是由操作系统提供的通用、高速跟踪设备。 它使用在内核中实现的缓冲和日志记录机制，为用户模式应用程序和内核模式设备驱动程序引发的事件提供跟踪机制。 此外，ETW 还可以动态启用和禁用日志记录，这样就可以轻松地在生产环境中执行详细跟踪，而无需重新启动或重新启动应用程序。 日志记录机制使用异步编写器线程写入磁盘的每个处理器缓冲区。 此缓冲允许大规模服务器应用程序写入具有最小干扰的事件。

ETW 是在 Windows 2000 中引入的。 自那时起，各种核心操作系统和服务器组件已采用 ETW 来检测其活动。 ETW 现在是 Windows 平台上的一项关键检测技术。 越来越多的第三方应用程序使用 ETW 进行检测，某些应用程序利用 Windows 提供的事件。 ETW 还已抽象到 Windows 预处理器 (WPP) 软件跟踪技术，该技术提供一组易于使用的宏，用于在开发期间跟踪 **printf**样式的消息进行调试。

ETW 对于 Windows Vista 和 Windows 7 进行了重大升级。 最重要的新功能之一是统一事件提供程序模型和 Api。 简而言之，新的统一 Api 将日志记录跟踪和写入事件查看器合并为事件提供程序的一个一致、易用的机制。 同时，为 ETW 增加了几项新功能，以改善开发人员和最终用户体验。

有关 ETW 和 WPP 的详细信息，请参阅 [Windows (etw) 的 ](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)事件跟踪和事件跟踪。

## <a name="usb-support-for-etw-logging"></a>支持 ETW 日志记录的 USB


USB 是将越来越多的外围设备连接到 Pc 的最流行的方法之一。 有一个非常大的安装 USB 主机电脑和 USB 外围设备的基础，以及系统供应商、设备供应商和最终用户希望并要求 USB 设备在系统和设备级别上正常运行。

USB 设备的大安装基础和增加数量在 Windows USB 软件堆栈、USB 主机控制器和 USB 设备之间出现兼容性问题。 这些兼容性问题会导致客户出现问题，例如设备操作故障、系统挂起和系统崩溃。

无需直接访问系统和/或设备，或在某些情况下系统崩溃转储，调查和调试 USB 设备问题是很困难或无法进行的。 即使有了对硬件和故障转储的完全访问权限，提取相关信息也是一种非常耗时的技术，只需几核的核心 USB 驱动程序开发人员即可。 您可以使用硬件或软件分析器调试 USB 问题，但这些问题非常昂贵，只可供少量专业人员使用。

## <a name="usb-etw-support-in-windows-7"></a>Windows 7 中的 USB ETW 支持


在 Windows 7 中，ETW 提供了一种事件日志记录机制，可以利用该机制来帮助调查、诊断和调试与 USB 相关的问题。 USB 驱动程序堆栈 ETW 事件日志记录支持 USB 驱动程序堆栈中现有 ad hoc 日志记录机制提供的大多数或全部调试功能，而没有任何限制。 这可以简化调试与 USB 相关的问题，该问题应在长期提供更可靠的 USB 驱动程序堆栈。

我们向 USB 主机控制器驱动程序和 Windows 7 中的 USB 集线器驱动程序添加了 ETW 日志记录。 USB 主机控制器驱动程序层包括主机控制器端口驱动程序 ( # A0) 和微型端口驱动程序 ( # A1、usbohci.sys 和 usbuhci.sys) 。 USB 集线器驱动程序层包含 USB 集线器驱动程序 ( # A0) 。 Windows 7 的所有版本和 Sku 中都包含 USB 驱动程序 ETW 事件提供程序。

-   USB 集线器事件

    启用 USB 事件收集后，USB 集线器事件提供程序会报告添加和删除 USB 集线器、所有集线器的设备摘要事件以及端口状态更改。 您可以使用这些事件来确定大多数设备枚举失败的根本原因。

-   USB 端口事件

    启用 USB 事件收集后，USB 端口事件提供程序将从客户端驱动程序、打开和关闭设备终结点以及微型端口状态转换（如微型端口启动和停止）报告 i/o。 记录的 i/o 包括对物理 USB 端口状态的请求。 物理 USB 端口上的状态转换是核心 USB 驱动程序堆栈中活动的关键发起程序之一。

## <a name="usb-etw-support-in-windows-8"></a>Windows 8 中的 USB ETW 支持


Windows 8 提供了 USB 驱动程序堆栈以支持 USB 3.0 设备。 Microsoft 提供的 USB 3.0 驱动程序堆栈包含三个驱动程序： Usbxhci.sys、Ucx01000.sys 和 Usbhub3.sys。 所有三个驱动程序一起工作，为大多数 USB 3.0 主机控制器向 Windows 添加本机支持。 新的驱动程序堆栈支持 SuperSpeed、高速、全速、全速的设备。 Windows 8 支持 USB 2.0 驱动程序堆栈。 通过事件跟踪，USB 3.0 驱动程序堆栈可以查看主机控制器及其连接到的所有设备的细化活动。

-   USB Hub3 事件

    启用 USB 事件收集后，USB Hub3 事件提供程序会报告添加和删除 USB 集线器、所有集线器的设备摘要事件、端口状态更改以及 USB 设备和集线器的电源状态。 端口状态更改是物理 USB 端口上的状态转换，是核心 USB 驱动程序堆栈中活动的关键发起程序之一。 Hub3 报告枚举过程的各个阶段，该过程指向根本原因导致大多数设备枚举失败。 启用 **StateMachine** 关键字后，Hub3 将报告软件设备、中心和端口对象的内部状态机活动，使其更深入地查看驱动程序的逻辑。

-   USB UCX 事件

    启用 USB 事件收集后，USB UCX 事件提供程序将从客户端驱动程序报告 i/o，并打开和关闭设备终结点和终结点流。 启用 **StateMachine** 关键字后，UCX 将报告主机控制器和终结点对象的内部状态机活动，从而更深入地查看驱动程序的逻辑。

-   USB xHCI 事件

    启用 USB 事件收集后，USB xHCI 事件提供程序将报告系统的 xHCI 控制器的属性和 xHCI 操作的低级详细信息。 xHCI 报告由 xHCI 硬件发送和完成的命令请求，包括特定于 xHCI 的完成代码。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md" data-raw-source="[Capture and view USB traces with Microsoft Message Analyzer](capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md)">使用 Microsoft Message Analyzer 捕获和查看 USB 跟踪</a></p></td>
<td><p>可以使用 Microsoft Message Analyzer (MMA) 来捕获和查看实时 USB 跟踪，或查看现有跟踪。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-capture-a-usb-event-trace.md" data-raw-source="[How to capture a USB event trace with Logman](how-to-capture-a-usb-event-trace.md)">如何使用 Logman 捕获 USB 事件跟踪</a></p></td>
<td><p>本主题提供有关使用 <a href="https://go.microsoft.com/fwlink/p/?linkid=617153" data-raw-source="[Logman](https://go.microsoft.com/fwlink/p/?linkid=617153)">Logman</a> 工具捕获 USB ETW 事件跟踪的信息。 Logman 是内置于 Windows 中的跟踪工具。 可以使用 Logman 将事件捕获到事件跟踪日志文件中。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-usb-etw.md" data-raw-source="[Using activity ID GUIDs in USB ETW traces](using-usb-etw.md)">使用 USB ETW 跟踪中的活动 ID GUID</a></p></td>
<td><p>本主题提供有关活动 ID Guid 的信息、如何将这些 Guid 添加到事件跟踪提供程序中，以及如何在 Netmon 中查看它们。</p></td>
</tr>
<tr class="even">
<td><p><a href="viewing-etw-traces-in-netmon.md" data-raw-source="[USB ETW traces in Netmon](viewing-etw-traces-in-netmon.md)">Netmon 中的 USB ETW 跟踪</a></p></td>
<td><p>可以使用 Microsoft 网络监视器（也称为 Netmon）查看 USB ETW 事件跟踪。 Netmon 不会自动分析跟踪。 它需要 USB ETW 分析。 USB ETW 分析器是以网络监视器分析器语言编写的文本文件， (NPL) ，用于描述 USB ETW 事件跟踪的结构。 分析器还会定义 USB 特定的列和筛选器。 这些分析器使 Netmon 成为分析 USB ETW 跟踪的最佳工具。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-xperf-with-usb-etw.md" data-raw-source="[Using Xperf with USB ETW](using-xperf-with-usb-etw.md)">将 Xperf 与 USB ETW 配合使用</a></p></td>
<td><p>本主题介绍如何将 Xperf 与 Netmon 配合使用来分析 USB 跟踪数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-etw-and-power-management.md" data-raw-source="[USB ETW and Power Management](usb-etw-and-power-management.md)">USB ETW 和电源管理</a></p></td>
<td><p>本主题简要概述了如何使用 ETW 来检查 USB 选择性挂起状态，并使用 Windows PowerCfg 实用工具确定系统能源效率问题。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[使用 USB ETW](using-usb-etw.md)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  



