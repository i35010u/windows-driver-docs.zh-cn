---
Description: 本主题提供信息的客户端驱动程序开发人员的跟踪和日志记录功能的通用串行总线 (USB)。
title: Windows 的 USB 事件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680a65744992420a7e333e4c6341ffff15f8d02d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356589"
---
# <a name="usb-event-tracing-for-windows"></a>Windows 的 USB 事件跟踪


本主题提供信息的客户端驱动程序开发人员的跟踪和日志记录功能的通用串行总线 (USB)。 为了方便开发和调试 USB 设备的人员提供此信息。 它包括有关如何安装工具、 创建跟踪文件和分析 USB 跟踪文件中的事件的信息。 本主题假定你已成功使用 USB 跟踪和日志记录功能所需的硬件的 USB 生态系统的全面了解。

若要解释的事件跟踪，您还必须了解 Windows [USB 宿主端驱动程序在 Windows 中的](usb-3-0-driver-stack-architecture.md)，则[官方 USB 规范和 USB 设备类规范](https://www.usb.org/documents)。

-   [有关 Windows 事件跟踪](#about-event-tracing-for-windows)
-   [ETW 日志记录的 USB 支持](#usb-support-for-etw-logging)
-   [在 Windows 7 USB ETW 支持](#usb-etw-support-in-windows-7)
-   [Windows 8 中的 USB ETW 支持](#usb-etw-support-in-windows-8)

## <a name="about-event-tracing-for-windows"></a>有关 Windows 事件跟踪


Windows 事件跟踪 (ETW) 是一种高速通用的跟踪工具，由操作系统提供。 它使用缓冲和日志记录机制，在要提供用于用户模式应用程序和内核模式设备驱动程序引发的事件的跟踪机制的内核中实现。 此外，ETW 提供了能够动态启用和禁用日志记录，这样，就可以轻松地在生产环境中执行详细的跟踪，而无需重新启动或应用程序重新启动。 日志记录机制使用每个处理器缓冲区写入磁盘的异步编写器线程。 此缓冲，大规模服务器应用程序在写入事件时最小的干扰。

在 Windows 2000 中引入 ETW。 从那时起，各种核心的操作系统和服务器组件开始纷纷采用 ETW 其活动进行检测。 ETW 现在是 Windows 平台上的主要检测技术之一。 越来越多的第三方应用程序使用 ETW 进行检测，并且一些利用 Windows 提供的事件。 ETW 还被提取到的 Windows 预处理器 (WPP) 软件跟踪技术，它为跟踪提供的一组易于使用宏**printf**-样式在开发期间调试消息。

ETW 得到重要升级适用于 Windows Vista 和 Windows 7。 最重要的新功能之一是统一的事件提供程序模型和 Api。 简单地说，新的统一的 Api 结合使用日志记录跟踪和事件查看器写入到一个一致的、 易于使用的事件提供程序的机制。 同时，在多项新功能已添加到 ETW 来提高开发人员和最终用户体验。

有关 ETW 和 WPP 的详细信息，请参阅事件跟踪和[事件跟踪 Windows (ETW)](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)。

## <a name="usb-support-for-etw-logging"></a>ETW 日志记录的 USB 支持


USB 是不断增加的各种外围设备连接到电脑的最常见方式之一。 没有非常大的客户的群，USB 宿主 Pc 和 USB 外围设备和系统供应商，设备供应商和最终用户期望和要求在系统和设备级别完美运行 USB 设备。

大的客户的群和 USB 设备的激增已发现的 Windows USB 软件堆栈、 USB 主控制器和 USB 设备之间的兼容性问题。 这些兼容性问题会导致设备操作失败、 系统挂起和系统崩溃等的客户的问题。

很难或无法进行调查和调试系统故障转储的 USB 设备问题，而无需直接访问系统，和/或设备，或在某些情况下。 即使使用完全访问权限的硬件要求和故障转储，提取相关的信息已被已知仅通过几个核心 USB 驱动程序开发人员的需要进行大量时间的技术。 您可以通过使用硬件或软件分析器调试 USB 问题，但它们会占用大量资源，适用于只有极少比例的专业人员。

## <a name="usb-etw-support-in-windows-7"></a>在 Windows 7 USB ETW 支持


在 Windows 7 中，ETW 提供了事件日志记录机制，可以利用 USB 驱动程序堆栈，以帮助调查、 诊断和调试 USB 相关的问题。 USB 驱动程序堆栈 ETW 事件日志记录支持大多数或所有调试功能所提供的 USB 驱动程序堆栈，而无需任何其自身的局限性中的现有临时日志记录机制。 这将转化为方便调试 USB 相关问题，应在长期内提供更可靠的 USB 驱动程序堆栈。

我们添加了 ETW 日志记录到 USB 主控制器驱动程序和 Windows 7 中的 USB 集线器驱动程序。 USB 主机控制器驱动程序层包括主机控制器端口驱动程序 (usbport.sys) 和 （usbehci.sys、 usbohci.sys 和 usbuhci.sys） 的微型端口驱动程序。 USB 集线器驱动程序层包含 USB 集线器驱动程序 (usbhub.sys)。 USB 驱动程序 ETW 事件提供程序包含在所有版本和 Windows 7 的 Sku。

-   USB 集线器事件

    启用 USB 事件收集时，USB 集线器事件提供程序报告的添加和删除的 USB 集线器、 设备摘要事件的所有中心和端口的状态更改。 这些事件可用于确定的大多数设备枚举失败的根本原因。

-   USB 端口事件

    启用 USB 事件收集时，USB 端口事件提供程序报告 I/O 从客户端驱动程序，打开和关闭的设备的终结点，并如微型端口的微型端口状态转换启动和停止。 记录的 I/O 包括物理 USB 端口的状态的请求。 物理 USB 端口上的状态转换是活动的一种核心 USB 驱动程序堆栈中的密钥发起程序。

## <a name="usb-etw-support-in-windows-8"></a>Windows 8 中的 USB ETW 支持


Windows 8 提供的 USB 驱动程序堆栈，以支持 USB 3.0 设备。 Microsoft 提供的 USB 3.0 驱动程序堆栈包含三个的驱动程序：Usbxhci.sys、 Ucx01000.sys 和 Usbhub3.sys。 所有三个的驱动程序协同工作来为大多数 USB 3.0 主机控制器添加到 Windows 的本机支持。 新的驱动程序堆栈支持 SuperSpeed，高速、 最快速度和较慢的设备。 在 Windows 8 上支持 USB 2.0 驱动程序堆栈。 事件跟踪通过 USB 3.0 驱动程序堆栈提供的主控制器和所有设备连接到它的精细活动视图。

-   USB Hub3 事件

    启用 USB 事件收集时，USB Hub3 事件提供程序报告的添加和删除的 USB 集线器、 所有中心、 端口状态更改和 USB 设备和集线器的电源状态的设备摘要事件。 端口状态更改是物理的 USB 端口上的状态转换，并且其中一个核心 USB 驱动程序堆栈中的活动的密钥发起程序。 Hub3 报告枚举过程中，指向根的阶段会导致大多数设备枚举失败。 与**StateMachine**关键字启用，Hub3 报告软件设备、 中心和 port 对象，提供更深入地洞察驱动程序的逻辑的内部状态机活动。

-   USB UCX 事件

    启用 USB 事件收集时，USB UCX 事件提供程序将报告从客户端驱动程序和打开和关闭设备终结点和终结点流的 I/O。 与**StateMachine**关键字启用，UCX 报告内部状态机活动的主机控制器和终结点对象，提供更深入地洞察驱动程序的逻辑。

-   USB xHCI 事件

    启用 USB 事件收集时，USB xHCI 事件提供程序报告的属性系统的 xHCI 控制器和 xHCI 操作的低级别详细信息。 xHCI 报告命令请求发送到和完成的 xHCI 硬件，包括特定于 xHCI 的完成代码。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md" data-raw-source="[Capture and view USB traces with Microsoft Message Analyzer](capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-.md)">使用 Microsoft Message Analyzer 捕获和查看 USB 跟踪</a></p></td>
<td><p>可以使用 Microsoft 消息分析器 (MMA) 来捕获和查看实时 USB 跟踪，或查看现有跟踪。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-capture-a-usb-event-trace.md" data-raw-source="[How to capture a USB event trace with Logman](how-to-capture-a-usb-event-trace.md)">如何捕获使用 Logman USB 事件跟踪</a></p></td>
<td><p>本主题提供有关使用信息<a href="https://go.microsoft.com/fwlink/p/?linkid=617153" data-raw-source="[Logman](https://go.microsoft.com/fwlink/p/?linkid=617153)">Logman</a>工具，用于捕获的 USB ETW 事件跟踪。 Logman 是内置于 Windows 的跟踪工具。 可以使用 Logman 捕获到事件跟踪日志文件的事件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-usb-etw.md" data-raw-source="[Using activity ID GUIDs in USB ETW traces](using-usb-etw.md)">使用 USB ETW 跟踪中的活动 ID Guid</a></p></td>
<td><p>本主题介绍有关活动 ID Guid，如何添加这些 Guid 在事件跟踪提供程序，以及在网络监视器中查看它们。</p></td>
</tr>
<tr class="even">
<td><p><a href="viewing-etw-traces-in-netmon.md" data-raw-source="[USB ETW traces in Netmon](viewing-etw-traces-in-netmon.md)">网络监视器中的 USB ETW 跟踪</a></p></td>
<td><p>您可以查看使用 Microsoft 网络监视器，也称为 Netmon USB ETW 事件跟踪。 网络监视器不会自动分析跟踪。 它需要 USB ETW 分析程序。 USB ETW 分析器是文本文件，编写在网络监视器分析器语言 (NPL)，用于描述 USB ETW 事件跟踪的结构。 分析器还定义特定于 USB 的列和筛选器。 这些分析器进行 Netmon 分析 USB ETW 跟踪的最佳工具。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-xperf-with-usb-etw.md" data-raw-source="[Using Xperf with USB ETW](using-xperf-with-usb-etw.md)">使用 USB ETW 使用 Xperf</a></p></td>
<td><p>本主题介绍如何使用 Netmon Xperf 分析 USB 跟踪数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-etw-and-power-management.md" data-raw-source="[USB ETW and Power Management](usb-etw-and-power-management.md)">USB ETW 和电源管理</a></p></td>
<td><p>本主题提供了一条简短大致了解使用 ETW 来检查 USB 选择性挂起状态和使用 Windows PowerCfg 实用程序确定系统能源效率问题。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[使用 USB ETW](using-usb-etw.md)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  



