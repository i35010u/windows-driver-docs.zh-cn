---
title: TCPMON Xcv 命令
description: TCPMON Xcv 命令
ms.assetid: 89aebc89-d81e-4d86-942e-d13b16c55fb3
keywords:
- 打印监视器 WDK，TCPMON Xcv
- 收发 (Xcv) 命令 WDK 打印
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
ms.openlocfilehash: 643b9e4cd2aaa4570b0ea72ca4f6ab9c9f053c68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554250"
---
# <a name="tcpmon-xcv-commands"></a>TCPMON Xcv 命令





本部分介绍可以在调用中指定的命令[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)或[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)时它是函数与标准 TCP/IP 端口监视器 (TCPMON) 进行通信。 通过指定每个命令*pszDataName*对这些函数的调用中的字符串。 某些命令要求输入的缓冲区，或输出缓冲区，或这两者。 *PInputData*并*pOutputData*这些函数的参数保存这些缓冲区的地址。

在每个以下的说明中出现的表的命令列表**XcvData**并**XcvDataPort**与命令一起使用的参数。 请注意， *hXcv*参数 （共有两个函数） 未列出，也不是**XcvData**函数的*pdwStatus*参数。

### <a name="addport-command"></a>端口命令

**端口**命令将添加标准的 TCP/IP 端口，可以是 LPR 端口或原始 TCP/IP 端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;AddPort&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>地址<a href="https://msdn.microsoft.com/library/windows/hardware/ff559892" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559892)"> <strong>PORT_DATA_1</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>一个 dword 值的地址</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_如果可以将该端口添加的错误。 正常的错误代码，除了**XcvData**将返回错误\_访问\_拒绝用户是否有权限不足，无法在服务器上创建一个端口。 此命令需要服务器\_访问\_管理特权。 如果*pInputData*参数是**NULL**，该函数将返回错误\_无效\_数据。 如果*pInputData*--&gt;*dw 版本*不是等于 1，函数将返回错误\_无效\_级别。

### <a name="configport-command"></a>ConfigPort 命令

**ConfigPort**命令将配置一个现有的标准 TCP/IP 端口监视器端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;ConfigPort&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>地址<a href="https://msdn.microsoft.com/library/windows/hardware/ff559892" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559892)"> <strong>PORT_DATA_1</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>一个 dword 值的地址</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_错误如果它可以配置的端口。 正常的错误代码，除了**XcvData**将返回错误\_访问\_拒绝如果调用方没有足够的特权，无法执行请求。 此命令需要服务器\_访问\_管理特权。 如果*pInputData*参数是**NULL**，或中的值*cbInputData*较小不是必需的该函数将返回错误\_无效\_数据。 如果*pInputData*--&gt;*dw 版本*不是等于 1，函数将返回错误\_无效\_级别。

### <a name="deleteport-command"></a>DeletePort 命令

**DeletePort**命令从标准 TCP/IP 端口监视器中删除一个端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;DeletePort&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>地址<a href="https://msdn.microsoft.com/library/windows/hardware/ff547436" data-raw-source="[&lt;strong&gt;DELETE_PORT_DATA_1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547436)"> <strong>DELETE_PORT_DATA_1</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(DELETE_PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>一个 dword 值的地址</p></td>
</tr>
</tbody>
</table>

 

**XcvData**会返回任何\_错误，如果已成功删除该端口。 正常的错误代码，除了**XcvData**将返回错误\_访问\_拒绝调用方在服务器上具有足够的特权。 此命令需要服务器\_访问\_管理特权。 如果*pInputData*参数是**NULL**，或者，如果*cbInputData*小于所需参数，该函数将返回错误\_无效\_数据。 如果*pInputData*--&gt;*dw 版本*不是等于 1，函数将返回错误\_无效\_级别。

### <a name="getconfiginfo-command"></a>GetConfigInfo 命令

**GetConfigInfo**命令中获得的特定端口的配置信息。 在这种情况下，Xcv 数据句柄必须指向一个特定的标准 TCP/IP 端口号监视器端口，以便可以识别该端口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;GetConfigInfo&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p>地址<a href="https://msdn.microsoft.com/library/windows/hardware/ff546300" data-raw-source="[&lt;strong&gt;CONFIG_INFO_DATA_1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546300)"> <strong>CONFIG_INFO_DATA_1</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p><strong>sizeof</strong>(CONFIG_INFO_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>地址<a href="https://msdn.microsoft.com/library/windows/hardware/ff559892" data-raw-source="[&lt;strong&gt;PORT_DATA_1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559892)"> <strong>PORT_DATA_1</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(PORT_DATA_1)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>指向包含所需的缓冲区的字节数的 DWORD 地址<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

**XcvData**会返回任何\_错误如果它可以获取该端口的配置信息。 如果*pInputData*是**NULL**，或者，如果*cbInputData*较小不是必需的该函数将返回错误\_无效\_数据。 如果*pInputData*--&gt;*dw 版本*不是等于 1，函数将返回错误\_无效\_级别。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。

### <a name="hostaddress-command"></a>主机地址命令

**主机地址**命令将获取打印机的主机名。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;HostAddress&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机的字符串的缓冲区的地址&#39;的主机名</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>指向缓冲区的大小<em>pOutputData</em></p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>指向包含所需的缓冲区的字节数的 DWORD 地址<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_错误如果它可以获得打印机的主机的名称。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

### <a name="ipaddress-command"></a>IPAddress 命令

**IPAddress**命令将获取打印机的 IP 地址。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;IPAddress&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机的字符串的缓冲区的地址&#39;IP 地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>指向缓冲区的大小<em>pOutputData</em></p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>指向包含所需的缓冲区的字节数的 DWORD 地址<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_错误如果它可以获得打印机的 IP 地址。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

### <a name="monitorui-command"></a>MonitorUI 命令

**MonitorUI**命令获取端口监视器 UI TCPMON 中提供的接口的 DLL 的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;MonitorUI&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
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
<td><p>中包含的端口监视器用户界面 DLL 名称的字符串的字节数</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>指向包含所需的缓冲区的字节数的 DWORD 地址<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_错误，如果能够获取用户的名称接口 DLL。 正常的错误代码，除了**XcvData**将返回错误\_访问\_拒绝调用方在服务器上具有足够的特权。 此命令需要服务器\_访问\_管理特权。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

### <a name="snmpcommunity"></a>SNMPCommunity

**SNMPCommunity**命令将获取打印机的简单网络管理协议 (SNMP) 社区名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;SNMPCommunity&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收包含打印机的字符串的缓冲区的地址&#39;s SNMP 团体</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p>指向包含字符串所需的缓冲区的大小<em>pOutputData</em>参数</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>指向包含所需的缓冲区的字节数的 DWORD 地址<em>pOutputData</em></p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_错误如果它可以获取打印机的 SNMP 社区名称。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

### <a name="snmpdeviceindex"></a>SNMPDeviceIndex

**SNMPDeviceIndex**命令将获取打印机的简单网络管理协议 (SNMP) 设备索引。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;SNMPDeviceIndex&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
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
<td><p><strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>地址包含一个 DWORD <strong>sizeof</strong>(DWORD)</p></td>
</tr>
</tbody>
</table>

 

[**XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)会返回任何\_如果它可以获取打印机的 SNMP 设备索引错误。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

### <a name="snmpenabled"></a>SNMPEnabled

**SNMPEnabled**命令确定是否为当前的设备启用了简单网络管理协议 (SNMP)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>XcvData 参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pszDataName</em></p></td>
<td><p>L&quot;SNMPEnabled&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>pInputData</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>cbInputData</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>pOutputData</em></p></td>
<td><p>接收的 DWORD 值的缓冲区的地址</p></td>
</tr>
<tr class="odd">
<td><p><em>cbOutputData</em></p></td>
<td><p><strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><em>pcbOutputNeeded</em></p></td>
<td><p>地址包含一个 DWORD <strong>sizeof</strong>(DWORD)</p></td>
</tr>
</tbody>
</table>

 

**XcvData**会返回任何\_如果为设备启用了 SNMP 的错误。 如果*cbOutputData*较小不是必需的该函数将返回错误\_无效\_参数时*pcbOutputNeeded*是**NULL**，和错误\_不足\_缓冲时*pcbOutputNeeded*为非**NULL**。 如果*pOutputData*是**NULL**，该函数将返回错误\_无效\_参数。

 

 




