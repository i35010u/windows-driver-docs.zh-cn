---
title: 打印驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义打印驱动程序的起点。
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 019935d35be1cf4a15b9c3541300bdd81cd15985
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785605"
---
# <a name="print-driver-samples"></a>打印驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义打印驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [打印自动配置](/samples/microsoft/windows-driver-samples/print-auto-configuration-sample) | 演示如何实现基于 Unidrv 和 PScript5 的驱动程序，以利用自动配置的收件箱支持。 此示例仅在与标准 TCP/IP 端口监视器或 Network-Connected 设备 (NCD) 端口监视器一起使用时才有效。 |
| [公共属性表 UI](/samples/microsoft/windows-driver-samples/common-property-sheet-ui-sample) | 导致公共属性表用户界面 (CPSUI) 的应用程序调用 Windows 打印后台处理程序，以便为系统的默认打印机创建属性表页。 |
| [OEM 打印机自定义插件示例](/samples/microsoft/windows-driver-samples/oem-printer-customization-plug-in-samples) | OEMDLL 示例演示了 OEM 自定义插件。BITMAP、OEMPS、OEMUI、OEMUNI、OEMPREAN、CUSTHLP、SyncSet、ThemeUI、PSUIRep 和水印示例不会影响打印机输出。 它们只是如何构建各种类型的 OEM 自定义 Dll 的示例。|
| [OpenXPS 文档](/samples/microsoft/windows-driver-samples/openxps-documents-print-sample) | 包含从各种源生成的一组文档，包括从 .NET Framework 中的 Windows Presentation Foundation 生成的文档和从 Microsoft XPS 文档编写器 (MXDW) 生成的文档。 其中提供了一些文档来演练 XML 纸张规范的各种功能。 |
| [XPS 文档](/samples/microsoft/windows-driver-samples/xps-documents-print-sample) | 包含从各种源生成的一组文档，包括从 .NET Framework 中的 Windows Presentation Foundation 生成的文档和从 Microsoft XPS 文档编写器 (MXDW) 生成的文档。 其中提供了一些文档来演练 XML 纸张规范的各种功能。 |
| [打印管道简单筛选器](/samples/microsoft/windows-driver-samples/print-pipeline-simple-filter) | 演示如何使用打印管道的筛选器接口。 |
| [打印机扩展](/samples/microsoft/windows-driver-samples/printer-extension-sample) | 演示如何使用 .NET 为 v4 打印驱动程序生成自定义的桌面 UI。 此 .NET 应用程序使用 PrintTicket、PrintCapabilities 和双向，以便与打印系统进行通信，并适合包含在 v4 打印驱动程序中。 |
| [打印驱动程序约束](/samples/microsoft/windows-driver-samples/print-driver-constraints-sample) | 演示如何实现高级约束处理，以及如何使用 JavaScript 实现 PrintTicket/PrintCapabilities 处理。  |
| [USB Host-Based 打印驱动程序](/samples/microsoft/windows-driver-samples/usb-host-based-print-driver-sample) | 演示如何支持使用 v4 打印驱动程序模型并通过 USB 连接的基于主机的设备。 |
| [打印 USB 监视器和双向](/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)  | 演示如何使用 JavaScript 和 XML 来支持通过 USB 总线进行双向 (双向) 通信。 在打印时，此示例支持双向状态，不能在打印时进行双向状态，也不支持打印机的状态。 |
| [WSDMon 双向扩展](/samples/microsoft/windows-driver-samples/wsdmon-bidi-extension-sample)  | 演示如何使用 XML 扩展文件来支持与 WSD 连接的打印机) 双向 (双向通信。 |
| [XPSDrv 驱动程序和筛选器](/samples/microsoft/windows-driver-samples/xpsdrv-driver-and-filter-sample) | 本示例旨在提供用于开发 XPSDrv 打印机驱动程序的起点，并说明 XPSDrv 打印驱动程序的功能和潜能。 这一目标是通过在一组 XPS 打印管道筛选器中实现的，这些功能是通过支持自定义 UI 内容和 PrintTicket 处理的配置插件配置的。 |
| [XPS 光栅化筛选器服务](/samples/microsoft/windows-driver-samples/xps-rasterization-filter-service-sample) | 用于栅格化 XPS 文档中的固定页面的 XPSDrv 筛选器。 硬件供应商可以修改此示例以生成一个 XPSDrv 筛选器，用于为其打印机或其他显示设备生成位图图像。 |
