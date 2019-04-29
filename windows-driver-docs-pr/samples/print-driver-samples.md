---
title: 打印驱动程序示例
description: 此目录中的驱动程序示例为编写你的设备的自定义打印驱动程序提供的起始点。
ms.assetid: B4485626-9062-4892-B317-8FFA8B68C0D0
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 900bfc1806e5cbbfdb548af810062ba8dc29e4fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366317"
---
# <a name="print-driver-samples"></a>打印驱动程序示例


此目录中的驱动程序示例为编写你的设备的自定义打印驱动程序提供的起始点。

## <a name="print"></a>Print


| 示例名称                      | 解决方案                                                                  | 描述  |
|----------------------------------|---------------------------------------------------------------------------|--------------|
| 打印自动配置         | [AutoConfig](https://go.microsoft.com/fwlink/p/?LinkId=617938)             | 演示如何实现基于 Unidrv 以及基于 PScript5 的驱动程序，以利用自动配置的收件箱支持。 此示例仅适用于与标准 TCP/IP 端口监视器或 Network-Connected 设备 (NCD) 端口监视器一起使用。                                                                                                                                                |
| UI 的常用属性表         | [cpsuisam](https://go.microsoft.com/fwlink/p/?LinkId=617940)               | 应用程序导致常用属性页用户界面 (CPSUI) 来调用 Windows 打印后台处理程序创建属性表页的系统的默认打印机。                                                                                                                                                                                                                       |
| OEM 打印机自定义项插件示例 | [OEM 打印机自定义项插件示例](https://go.microsoft.com/fwlink/?linkid=862105) | OEMDLL 示例都是举例说明了 OEM 自定义插件。位图、 OEMPS、 OEMUI、 OEMUNI、 OEMPREAN、 CUSTHLP、 SyncSet、 ThemeUI、 PSUIRep 和水印示例不会影响打印机输出。 它们是仅为示例演示如何生成各种类型的 OEM 自定义 Dll。               |
| OpenXPS 文档                | [SampleOpenXps](https://go.microsoft.com/fwlink/p/?LinkId=617941)          | 包含一组不同的源，包括生成从.NET Framework 中的 Windows Presentation Foundation 和 Microsoft XPS 文档编写器 (MXDW) 从数据源生成的文档。 它们包含了为你提供执行各种功能的 XML 纸张规范的几个文档。                                               |
| XPS 文档                    | [SampleXPS](https://go.microsoft.com/fwlink/p/?LinkId=617942)              | 包含一组不同的源，包括生成从.NET Framework 中的 Windows Presentation Foundation 和 Microsoft XPS 文档编写器 (MXDW) 从数据源生成的文档。 它们包含了为你提供执行各种功能的 XML 纸张规范的几个文档。                                               |
| 打印管道简单的筛选器     | [SimplePipelineFilter](https://go.microsoft.com/fwlink/p/?LinkId=617944)   | 演示如何使用打印管道的筛选器接口。                                                                                                                                                                                                                                                                                                                                             |
| 打印机扩展                | [PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945) | 演示如何使用.NET 构建的 v4 打印驱动程序的自定义桌面 UI。 此.NET 应用程序以便与打印系统进行通信使用 PrintTicket 和 PrintCapabilities Bidi 并且适合包含在 v4 打印驱动程序中。                                                                                                                                           |
| 打印驱动程序约束         | [ConstraintScript](https://go.microsoft.com/fwlink/p/?LinkId=617946)       | 演示如何实现高级的约束处理和也 PrintTicket/PrintCapabilities 处理使用 JavaScript。                                                                                                                                                                                                                                                                        |
| USB 基于主机的打印驱动程序      | [HostBasedSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=617947)  | 演示如何支持使用 v4 打印驱动程序模型，并通过 USB 连接的基于主机的设备。                                                                                                                                                                                                                                                                                        |
| 打印 USB 监视器和 BiDi       | [USBMon-Bidi-Extension](https://go.microsoft.com/fwlink/p/?LinkId=617948)  | 演示如何通过 USB 总线，使用 JavaScript 和 XML 支持双向 (Bidi) 通信。 此示例支持双向状态时无法打印和从打印机打印时未经请求的状态。                                                                                                                                                                     |
| WSDMon Bidi 扩展            | [WSDMon-Bidi-Extension](https://go.microsoft.com/fwlink/p/?LinkId=617949)  | 演示如何使用 XML 扩展文件以支持与 WSD 连接打印机的双向 (Bidi) 通信。                                                                                                                                                                                                                                                                            |
| XPSDrv 驱动程序和筛选器         | [XPSDrvSmpl](https://go.microsoft.com/fwlink/p/?LinkId=617950)             | 此示例旨在用于开发 XPSDrv 的打印机驱动程序提供一个起始点并以阐释的设施和 XPSDrv 打印机驱动程序的潜力。 这一目标通过实现一组通过插件的配置，支持自定义 UI 内容和 PrintTicket 处理配置的 XPS 打印的管道筛选器中的实际功能很多。 |
| XPS 光栅化筛选器服务 | [XpsRasFilter](https://go.microsoft.com/fwlink/p/?LinkId=617951)           | 光栅 XPS 文档中固定页 XPSDrv 筛选器。 硬件供应商可以修改此示例，以便构建生成他们的打印机或其他显示设备的位图图像的 XPSDrv 筛选器。                                                                                                                                                                                          |





