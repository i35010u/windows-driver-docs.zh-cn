---
title: V4 驱动程序连接体系结构
description: V4 打印驱动程序模型提供了大量的支持以通过双向架构，简称为 Bidi 的双向通信。
ms.assetid: ED7C4A2D-449E-4271-9348-86EAC03B6E64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2f024cff5407861a744ccc4ce98e990836fa01c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556167"
---
# <a name="v4-driver-connectivity-architecture"></a>V4 驱动程序连接体系结构


V4 打印驱动程序模型中的连接组件的主要目标是提供通过双向架构，有时简称为 Bidi 的双向通信的丰富支持。

V4 打印驱动程序模型支持到 v3 打印驱动程序模型进行比较的简化的连接堆栈。

**端口监视器和语言监视器**

在 v4 驱动程序模型中或使用打印类驱动程序不支持第三方端口监视器和语言监视器。 V4 打印驱动程序模型将继续使用 WSDMon Bidi 扩展文件格式，以及 SNMP Bidi 扩展文件格式。 新 v4 中是通过 USB 使用 USBMon Bidi 扩展 XML 文件和 JavaScript 文件支持 Bidi 的能力。

**双向架构**

下表显示了文件和你必须提供的具体取决于你想要支持的功能和为您的打印设备选择通信协议的类型的信息。

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
<th>任何扩展文件</th>
<th>Bidi 扩展名为的文件</th>
<th>增强的自动配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>USB</td>
<td><p>以下属性为 Bidi 架构填充的端口监视器：</p>
<p>\Printer.DeviceInfo:Manufacturer</p>
<p>\Printer.DeviceInfo:ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo:SerialNumber</p></td>
<td><p>必须提供以下文件：</p>
- XML Bidi 扩展文件-JavaScript Bidi 扩展文件</td>
<td>打印设备必须支持此功能，必须提供 Bidi 扩展名为的文件。</td>
</tr>
<tr class="even">
<td>WSD</td>
<td>中的标准属性<a href="https://msdn.microsoft.com/library/windows/hardware/gg463146.aspx" data-raw-source="[WS-Print Specification](https://msdn.microsoft.com/library/windows/hardware/gg463146.aspx)">WS 打印规范</a>或 Ws-print v1.1 规范为 Bidi 架构填充的端口监视器。</td>
<td><p>必须提供以下文件：</p>
XML Bidi 扩展文件</td>
<td>打印设备必须支持 Ws-print v1.1 协议。</td>
</tr>
<tr class="odd">
<td>TCP/IP (SNMP)</td>
<td><p>如果实现端口监视器 MIB，然后以下属性填充到 Bidi 架构的端口监视器：</p>
<p>\Printer.DeviceInfo:Manufacturer</p>
<p>\Printer.DeviceInfo:ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo.NetworkingInfo:PresentationUrl</p>
<p>\Printer.Configuration.Memory:Size</p>
<p>\Printer.Configuration.HardDisk:Installed</p>
<p>\Printer.Configuration.DuplexUnit:Installed</p></td>
<td><p>必须提供以下文件：</p>
XML Bidi 扩展文件</td>
<td>打印设备必须支持此功能，必须提供 Bidi 扩展名为的文件。</td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[双向通信架构](https://msdn.microsoft.com/library/windows/hardware/ff545169.aspx)并[WSDMon 端口监视器](wsdmon-port-monitor.md)。 若要阅读有关自定义端口监视器，以扩展 Bidi 架构信息，请参阅[自定义打印机端口监视器](https://msdn.microsoft.com/library/windows/hardware/ff547327.aspx)。

## <a name="related-topics"></a>相关主题
[双向通信架构](https://msdn.microsoft.com/library/windows/hardware/ff545169.aspx)  
[自定义的打印机端口监视器](https://msdn.microsoft.com/library/windows/hardware/ff547327.aspx)  
[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)  
[WSDMon 端口监视器](wsdmon-port-monitor.md)  



