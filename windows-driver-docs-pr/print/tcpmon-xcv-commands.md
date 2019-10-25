---
title: TCPMON Xcv 命令
description: TCPMON Xcv 命令
ms.assetid: 89aebc89-d81e-4d86-942e-d13b16c55fb3
keywords:
- 打印监视器 WDK，TCPMON Xcv
- transceive （Xcv）命令 WDK 打印
- Xcv 命令 WDK 打印
- TCPMON Xcv 命令 WDK 打印
- AddPort
- ConfigPort
- DeletePort
- GetConfigInfo
- HostAddress
- IPAddress
- MonitorUI
- SNMPCommunity
- SNMPDeviceIndex
- SNMPEnabled
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a965b72820bc68fe94081d6c57b713de4fc56e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838785"
---
# <a name="tcpmon-xcv-commands"></a>TCPMON Xcv 命令





本部分介绍当使用[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))或[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)函数进行通信时，可以在对该函数的调用中指定的命令。 每个命令均由调用这些函数的*pszDataName*字符串指定。 某些命令需要输入缓冲区或输出缓冲区。 这些函数的*pInputData*和*pOutputData*参数包含这些缓冲区的地址。

以下每个命令的说明中显示的表列出了与命令一起使用的**XcvData**和**XcvDataPort**参数。 请注意， *hXcv*参数（对于这两个函数通用）未列出，也不是**XcvData**函数的*pdwStatus*参数。

### <a name="addport-command"></a>AddPort 命令

**AddPort**命令添加标准 tcp/ip 端口，此端口可以是 LPR 端口，也可以是原始 tcp/ip 端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "AddPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>结构的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>（PORT_DATA_1）</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))可以添加端口，则不会返回任何\_错误。 除了正常错误代码外，如果用户没有足够的权限在服务器上创建端口， **XcvData**将返回错误\_访问\_被拒绝。 此命令要求服务器\_访问\_管理权限。 如果*pInputData*参数为**NULL**，则该函数将返回错误\_无效的\_数据。 如果*pInputData*--&gt;*dwVersion*不等于1，则该函数将返回错误\_无效\_级别。

### <a name="configport-command"></a>ConfigPort 命令

**ConfigPort**命令配置现有的标准 tcp/ip 端口监视器端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "ConfigPort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>结构的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>（PORT_DATA_1）</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))可以配置端口，则不会返回任何\_错误。 除了正常错误代码外，如果调用方没有足够的权限来执行请求， **XcvData**会返回错误\_访问\_拒绝。 此命令要求服务器\_访问\_管理权限。 如果*pInputData*参数为**NULL**，或*cbInputData*中的值小于必需的值，则该函数将返回错误\_无效的\_数据。 如果*pInputData*--&gt;*dwVersion*不等于1，则该函数将返回错误\_无效\_级别。

### <a name="deleteport-command"></a>DeletePort 命令

**DeletePort**命令从标准 tcp/ip 端口监视器中删除端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "DeletePort"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_delete_port_data_1" data-raw-source="[&lt;strong&gt;DELETE_PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_delete_port_data_1)"><strong>DELETE_PORT_DATA_1</strong></a>结构的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>（DELETE_PORT_DATA_1）</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果成功删除了端口， **XcvData**将不会返回\_错误。 除了正常错误代码外，如果调用方在服务器上没有足够的权限， **XcvData**会返回错误\_访问\_被拒绝。 此命令要求服务器\_访问\_管理权限。 如果*pInputData*参数为**NULL**，或者*cbInputData*参数小于所需的参数，则函数将返回错误\_无效的\_数据。 如果*pInputData*--&gt;*dwVersion*不等于1，则该函数将返回错误\_无效\_级别。

### <a name="getconfiginfo-command"></a>GetConfigInfo 命令

**GetConfigInfo**命令获取特定端口的配置信息。 在这种情况下，Xcv 数据句柄必须指向特定的标准 TCP/IP 端口监视器端口，才能识别端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "GetConfigInfo"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_config_info_data_1" data-raw-source="[&lt;strong&gt;CONFIG_INFO_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_config_info_data_1)"><strong>CONFIG_INFO_DATA_1</strong></a>结构的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>（CONFIG_INFO_DATA_1）</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/tcpxcv/ns-tcpxcv-_port_data_1)"><strong>PORT_DATA_1</strong></a>结构的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>（PORT_DATA_1）</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<em>pOutputData</em>所指向的缓冲区所需的字节数的 DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果**XcvData**可以获取端口的配置信息，则它将不会返回任何\_错误。 如果*pInputData*为**NULL**，或*cbInputData*小于 REQUIRED，则函数将返回错误\_无效的\_数据。 如果*pInputData*--&gt;*dwVersion*不等于1，则该函数将返回错误\_无效\_级别。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。

### <a name="hostaddress-command"></a>HostAddress 命令

**HostAddress**命令获取打印机的主机名。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "HostAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机主机名的字符串的缓冲区地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><em>POutputData</em>所指向的缓冲区大小</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<em>pOutputData</em>所指向的缓冲区所需的字节数的 DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))可以获取打印机主机的名称，则不会返回任何\_错误。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

### <a name="ipaddress-command"></a>IPAddress 命令

**IPAddress**命令获取打印机的 IP 地址。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "IPAddress"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机 IP 地址的字符串的缓冲区地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><em>POutputData</em>所指向的缓冲区大小</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<em>pOutputData</em>所指向的缓冲区所需的字节数的 DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))可以获取打印机的 IP 地址，则不会返回任何\_错误。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

### <a name="monitorui-command"></a>MonitorUI 命令

**MonitorUI**命令获取提供 TCPMON 接口的端口监视器 UI DLL 的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "MonitorUI"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收端口监视器用户界面 DLL 名称的缓冲区的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>字符串中包含端口监视器用户界面 DLL 名称的字节数</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<em>pOutputData</em>所指向的缓冲区所需的字节数的 DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))能够获取用户界面 DLL 的名称，则不会返回任何\_错误。 除了正常错误代码外，如果调用方在服务器上没有足够的权限， **XcvData**会返回错误\_访问\_被拒绝。 此命令要求服务器\_访问\_管理权限。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

### <a name="snmpcommunity"></a>SNMPCommunity

**SNMPCommunity**命令获取打印机的简单网络管理协议（SNMP）团体名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "SNMPCommunity"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机 SNMP 社区的字符串的缓冲区的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>包含<em>pOutputData</em>参数指向的字符串所需的缓冲区大小</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<em>pOutputData</em>所指向的缓冲区所需的字节数的 DWORD 地址</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))可以获取打印机的 SNMP 团体名称，则不会返回任何\_错误。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

### <a name="snmpdeviceindex"></a>SNMPDeviceIndex

**SNMPDeviceIndex**命令获取打印机的简单网络管理协议（SNMP）设备索引。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "SNMPDeviceIndex"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收设备索引的缓冲区的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>（DWORD）</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<strong>sizeof</strong>的 dword 的地址（dword）</p></td>
</tr>
</tbody>
</table>

 

如果[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))无法获取打印机的 SNMP 设备索引，则不会返回任何\_错误。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

### <a name="snmpenabled"></a>SNMPEnabled

**SNMPEnabled**命令确定是否为当前设备启用了简单网络管理协议（SNMP）。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L "SNMPEnabled"</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收 DWORD 值的缓冲区的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>（DWORD）</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>包含<strong>sizeof</strong>的 dword 的地址（dword）</p></td>
</tr>
</tbody>
</table>

 

如果为设备启用了 SNMP，则**XCVDATA**不会返回\_错误。 如果*cbOutputData*小于所需的值，则当*pcbOutputNeeded*为**NULL**时，函数将返回错误\_无效的\_参数; 当*PCBOUTPUTNEEDED*是非时，\_缓冲区的错误\_**NULL**。 如果*pOutputData*为**NULL**，则函数将返回错误\_无效\_参数。

 

 




