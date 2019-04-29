---
title: 使用注册表值启用和禁用任务卸载
description: 使用注册表值启用和禁用任务卸载
ms.assetid: 32efd685-365c-4347-9599-fe429569d35b
keywords:
- 任务卸载，WDK TCP/IP 传输，注册表值
- 注册表 WDK TCP/IP 卸载
- 任务卸载，WDK TCP/IP 传输，启用服务
- 任务卸载，WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cceb9b5b163ebe8750402363c42a074edf202c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373767"
---
# <a name="using-registry-values-to-enable-and-disable-task-offloading"></a>使用注册表值启用和禁用任务卸载





在调试时驱动程序的任务卸载的功能，你可能会发现可以启用或禁用任务卸载服务使用注册表项设置。 没有你可以定义在 INF 文件和注册表中的标准化的关键字。 有关标准化关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

任务卸载关键字属于两个组之一： 精细关键字或分组的关键字。 *精细关键字*提供每个卸载功能-传输层差异化、 IP 协议差异化的关键字。 *分组关键字*提供组合的关键字在传输层的功能。

精细关键字定义，如下所示：

<a href="" id="-ipchecksumoffloadipv4"></a>**\*IPChecksumOffloadIPv4**  
介绍设备是启用还是禁用 IPv4 校验和计算。

<a href="" id="-tcpchecksumoffloadipv4"></a>**\*TCPChecksumOffloadIPv4**  
介绍设备是启用还是禁用通过 IPv4 数据包的 TCP 校验和计算。

<a href="" id="-tcpchecksumoffloadipv6"></a>**\*TCPChecksumOffloadIPv6**  
介绍设备是启用还是禁用通过 IPv6 数据包的 TCP 校验和计算。

<a href="" id="-udpchecksumoffloadipv4"></a>**\*UDPChecksumOffloadIPv4**  
介绍设备是启用还是禁用通过 IPv4 数据包的 UDP 校验和计算。

<a href="" id="-udpchecksumoffloadipv6"></a>**\*UDPChecksumOffloadIPv6**  
介绍设备是启用还是禁用通过 IPv6 数据包的 UDP 校验和计算。

<a href="" id="-lsov1ipv4"></a>**\*LsoV1IPv4**  
介绍设备是启用还是禁用的大型 TCP 数据包分段 IPv4 上的大量发送卸载版本 1 (LSOv1)。

<a href="" id="-lsov2ipv4"></a>**\*LsoV2IPv4**  
介绍设备是启用还是禁用的大型 TCP 数据包分段通过 IPv4 大量发送卸载版本 2 (LSOv2)。

<a href="" id="-lsov2ipv6"></a>**\*LsoV2IPv6**  
介绍设备是启用还是禁用的大型 TCP 数据包分段通过 IPv6 大量发送卸载版本 2 (LSOv2)。

<a href="" id="-ipsecoffloadv1ipv4"></a>**\*IPsecOffloadV1IPv4**  
介绍设备是启用还是禁用 IPsec 标头的计算通过 IPv4。

<a href="" id="-ipsecoffloadv2"></a>**\*IPsecOffloadV2**  
介绍设备是启用还是禁用 IPsec 卸载版本 2 (IPsecOV2)。 IPsecOV2 提供对其他加密算法、 IPv6 和与大量发送卸载版本 2 (LSOv2) 共存的支持。

<a href="" id="-ipsecoffloadv2ipv4"></a>**\*IPsecOffloadV2IPv4**  
介绍设备是启用还是禁用 IPsecOV2 仅 IPv4。

下表介绍可用于配置卸载服务的精细关键字。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>IPv4 校验和卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>TCPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>UDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>UDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>UDP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Rx &amp; Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV1IPv4</strong></p></td>
<td align="left"><p>大量发送卸载版本 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>LsoV2IPv4</strong></p></td>
<td align="left"><p>大量发送卸载 V2 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>LsoV2IPv6</strong></p></td>
<td align="left"><p>大量发送卸载 V2 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>IPsecOffloadV1IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载版本 1 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>IPsecOffloadV2</strong></p></td>
<td align="left"><p>IPsec 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*IPsecOffloadV2IPv4</strong></p></td>
<td align="left"><p>IPsec 卸载 (仅 IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用身份验证标头</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用的 ESP</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>身份验证标头&amp;ESP 启用</p></td>
</tr>
</tbody>
</table>

 

**请注意**  INF 文件可支持精细的 UI 的高级属性页中显示的关键字。 微型端口驱动程序必须所有精细设置从注册表中读取在初始化时，包括不会显示，以注册 NDIS 卸载功能的设置。

 

分组的关键字定义，如下所示：

<a href="" id="-tcpudpchecksumoffloadipv4"></a>**\*TCPUDPChecksumOffloadIPv4**  
介绍设备是启用还是禁用 IPv4 上的 IP、 TCP 和 UDP 校验和计算。

<a href="" id="-tcpudpchecksumoffloadipv6"></a>**\*TCPUDPChecksumOffloadIPv6**  
介绍设备是启用还是禁用 IPv6 上的 TCP 和 UDP 校验和计算。

下表介绍可用于配置卸载服务分组的关键字。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>TCPUDPChecksumOffloadIPv4</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Tx &amp; Rx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPUDPChecksumOffloadIPv6</strong></p></td>
<td align="left"><p>TCP/UDP 校验和卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Tx 启用</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Rx 启用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>Tx &amp; Rx 启用</p></td>
</tr>
</tbody>
</table>

 

没有限制的卸载，还可以启用组合。 例如，如果微型端口适配器支持 LSOV1 或 LSOV2，微型端口适配器也会计算 IP 和 TCP 校验和。 有关卸载的有效组合的详细信息，请参阅[合并类型的任务将卸载](combining-types-of-task-offloads.md)。

如果使用注册表项设置禁用了任务卸载服务，协议驱动程序必须发出[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)对象标识符 (OID)。

以下注册表值可用于启用或禁用任务卸载 TCP/IP 协议：

<a href="" id="hkey-local-machine-system-currentcontrolset-services-tcpip-parameters-disabletaskoffload-------"></a>**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\TCPIP\\Parameters\\DisableTaskOffload**   
此值设置为一个禁用所有任务将卸载从 TCP/IP 传输。 设置此值为零，所有任务卸载。

<a href="" id="hkey-local-machine-system-currentcontrolset-services-ipsec-enabledoffload-------"></a>**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\Ipsec\\EnabledOffload**   
此值设置为零禁止从 TCP/IP 传输 Internet 协议安全 (IPsec) 卸载。 TCP/IP 校验和任务卸载，大量发送卸载版本 1 (LSOV1)，以及大量发送卸载版本 2 (LSOV2) 不会受到影响。 此值设置为一个启用 IPsec 卸载。

 

 





