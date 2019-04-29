---
title: TCPMON Xcv 接口
description: TCPMON Xcv 接口
ms.assetid: 7b2b1cff-ab8f-44e0-9327-dc60a0072bf5
keywords:
- 打印监视器 WDK，TCPMON Xcv
- 收发 (Xcv) 接口 WDK 打印
- Xcv 接口 WDK 打印
- TCPMON Xcv 接口 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0e957fcc8682b79bc708cc6a932f6405fd5669b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388060"
---
# <a name="tcpmon-xcv-interface"></a>TCPMON Xcv 接口





本部分介绍标准 TCP/IP 端口监视器 (TCPMON) 收发 (Xcv) 接口。 此接口，使用实现[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)并[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)函数调用，使那些使用它来配置TCP/IP 打印机端口或要获得有关 TCP/IP 打印机端口配置的信息。 在本部分中所述的 Xcv 接口是特定的 TCP/IP 端口。 其他 Xcv 接口可能适用于其他端口类型。

若要获取本地计算机或远程计算机的 Xcv 接口的句柄，请调用**OpenPrinter**函数 （Microsoft Windows SDK 文档中所述）。 下面的代码示例说明了如何获取端口 Xcv 句柄：

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a local TCPMON port
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a TCPMON port on <ServerName>
}
```

在代码示例中， *ServerName*并*PortName*表示服务器和端口名称字符串。 一旦您获取句柄，您可以查询特定于 TCPMON 端口监视器的信息，或者可以更改端口配置。 请注意，必须以指定所需的端口监视器的访问权限**DesiredAccess**打印机的成员\_默认值结构 (或传递**NULL**如果需要任何特殊的安全性)。 对于某些调用[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数 (如时指定的端口和 DeletePort 命令-请参阅[TCPMON Xcv 命令](tcpmon-xcv-commands.md))，服务器\_访问\_是需要管理权限。 有关详细信息**OpenPrinter**函数，并可能在打印机中请求的访问权限\_默认结构，请参阅 Windows SDK 文档。

如果尚不存在该端口，Xcv 句柄可以是从服务器获取通过指定监视器名称。 （对于标准 TCP/IP 端口监视器端口，这是"标准 TCP/IP 端口"。）下面的代码示例说明了如何获取 Xcv 数据句柄端口监视器：

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor <MonitorName>
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor 
 // <MonitorName> on the server <ServerName>
}
```

在代码示例中， *ServerName*并*PortName*表示服务器和端口名称字符串。 一旦您获取 Xcv 数据句柄，您可以发出说明和请求监视器通过调用[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数。

请注意的返回值**XcvData**函数仅指示是否已正确地将数据发送到端口监视器。 返回值 **，则返回 TRUE**不指示操作是否成功。 若要确定操作是否成功，请检查中的值\* *pdwStatus*。 下表总结了这些状态的值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NO_ERROR</p></td>
<td><p>操作成功。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_ACCESS_DENIED</p></td>
<td><p>用户没有足够的特权。 该命令要求 SERVER_ACCESS_ADMINISTER 特权。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INSUFFICIENT_BUFFER</p></td>
<td><p>输出缓冲区是必需的但小于所需。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_DATA</p></td>
<td><p>输入的缓冲区是必需的但指针指向它<strong>NULL</strong>，或</p>
<p>输入缓冲区的大小小于所需。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_HANDLE</p></td>
<td><p>Xcv 数据句柄无效。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_LEVEL</p></td>
<td><p>输入或输出数据结构不是正确的版本。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_PARAMETER</p></td>
<td><p>输出缓冲区是必需的但很<strong>NULL</strong>，或</p>
<p>输出必需参数是<strong>NULL</strong>和输出缓冲区因过小，或</p>
<p>标准 TCP/IP 端口监视器不了解发出的命令。</p></td>
</tr>
</tbody>
</table>

 

 

 




