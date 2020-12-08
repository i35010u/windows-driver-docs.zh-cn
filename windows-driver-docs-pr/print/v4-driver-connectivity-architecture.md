---
title: V4 驱动程序连接体系结构
description: V4 打印驱动程序模型通过双向架构提供对双向通信的丰富支持，简称为双向。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58797621d2c9ab98bb8ec71928fbe3712e5ba1cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785935"
---
# <a name="v4-driver-connectivity-architecture"></a>V4 驱动程序连接体系结构


V4 打印驱动程序模型中连接组件的主要目标是通过双向架构为双向通信提供丰富的支持，有时称为 "双向"。

与 v3 打印驱动程序模型相比，v4 打印驱动程序模型支持简化的连接堆栈。

**端口监视器和语言监视器**

V4 驱动程序模型或打印类驱动程序不支持第三方端口监视器和语言监视器。 V4 打印驱动程序模型继续使用 WSDMon 双向扩展文件格式，以及 SNMP 双向扩展文件格式。 V4 中的新增功能是能够使用 USBMon 双向扩展 XML 和 JavaScript 文件在 USB 上支持双向。

**双向架构**

下表显示了必须提供的文件和信息，具体取决于你想要支持的功能以及你为打印设备选择的通信协议类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>通信类型</th>
<th>无扩展文件</th>
<th>双向扩展文件</th>
<th>增强的自动配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>USB</td>
<td><p>端口监视器将以下属性填充到双向架构中：</p>
<p>\Printer.DeviceInfo：制造商</p>
<p>\Printer.DeviceInfo： ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo： SerialNumber</p></td>
<td><p>您必须提供以下文件：</p>
- XML 双向扩展文件 - JavaScript 双向扩展文件</td>
<td>打印设备必须支持此功能，并且必须提供双向扩展文件。</td>
</tr>
<tr class="even">
<td>关于</td>
<td>来自 <a href="/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing" data-raw-source="[WS-Print Specification](/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing)">WS 打印规范</a> 或 WS-Print 1.1 规范的标准属性通过端口监视器填充到双向架构。</td>
<td><p>您必须提供以下文件：</p>
XML 双向扩展文件</td>
<td>打印设备必须支持 WS-Print 1.1 协议。</td>
</tr>
<tr class="odd">
<td>TCP/IP (SNMP) </td>
<td><p>如果已实现端口监视器 MIB，则端口监视器会将以下属性填充到双向架构中：</p>
<p>\Printer.DeviceInfo：制造商</p>
<p>\Printer.DeviceInfo： ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo.NetworkingInfo:PresentationUrl</p>
<p>\Printer.Configu。内存：大小</p>
<p>\Printer.Configu。硬盘：已安装</p>
<p>\Printer.Configu。DuplexUnit：已安装</p></td>
<td><p>您必须提供以下文件：</p>
XML 双向扩展文件</td>
<td>打印设备必须支持此功能，并且必须提供双向扩展文件。</td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [双向通信架构](./bidirectional-communication-schema.md) 和 [WSDMon 端口监视器](wsdmon-port-monitor.md)。 若要了解有关自定义端口监视器以扩展双向架构的信息，请参阅 [自定义打印机端口监视器](./customizing-the-printer-port-monitors.md)。

## <a name="related-topics"></a>相关主题
[双向通信架构](./bidirectional-communication-schema.md)  
[自定义打印机端口监视器](./customizing-the-printer-port-monitors.md)  
[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)  
[WSDMon 端口监视器](wsdmon-port-monitor.md)
