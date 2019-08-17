---
title: IP 帮助程序概述
description: IP 帮助程序概述
ms.assetid: c7cf1f47-ee0d-4c89-883b-717b719fcc2a
keywords:
- IP 帮助程序 WDK 网络
- IP 帮助程序 WDK 网络, 关于
- 网络驱动程序 WDK, IP 帮助程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaefca54c87eda5ec5b8aec6806cd7939b91b546
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565663"
---
# <a name="ip-helper-overview"></a>IP 帮助程序概述

Internet 协议帮助程序 (IP 帮助程序) 使驱动程序可以检索有关本地计算机的网络配置的信息并修改该配置。 IP 帮助程序还提供了通知机制, 以确保在本地计算机网络配置的某些方面发生更改时通知驱动程序。 IP 帮助程序在 Windows Vista 和更高版本的 Microsoft Windows 操作系统中可用。

许多 IP Helper 函数传递结构参数, 这些参数表示与管理信息基础 (MIB) 技术关联的数据类型。 IP Helper 函数使用这些 MIB 结构来表示不同的网络信息。

IP 帮助程序文档广泛使用术语 "适配器" 和 "接口"。 *适配器*是一种传统的术语, 它是*网络适配器*的缩写形式, 最初称为某种形式的网络硬件。 适配器是一个数据链接级别抽象。

作为抽象概念, 在 IETF RFC 文档中描述了一个*接口*, 表示某个节点与链接的连接。 接口是 IP 级抽象。

你的驱动程序可以使用以下内核模式函数、MIB 结构和 MIB 和网络层 (NL) 枚举来检索和修改本地计算机上传输控制协议/internet 协议 (TCP/IP) 传输的配置设置。

**请注意**  , 在开发驱动程序代码时, 请按照[包括头文件](including-header-files-for-ip-helper.md)的说明进行操作。

 

### <a name="interface-conversion-functions"></a>接口转换函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceAliasToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85))"><strong>ConvertInterfaceAliasToLuid</strong></a></p></td>
<td align="left"><p>将网络接口的本地唯一标识符 (LUID) 转换为 Unicode 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceGuidToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85))"><strong>ConvertInterfaceGuidToLuid</strong></a></p></td>
<td align="left"><p>将网络接口的全局唯一标识符 (GUID) 转换为接口的 LUID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceIndexToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85))"><strong>ConvertInterfaceIndexToLuid</strong></a></p></td>
<td align="left"><p>将网络接口的本地索引转换为接口的 LUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToAlias&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85))"><strong>ConvertInterfaceLuidToAlias</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为接口别名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToGuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85))"><strong>ConvertInterfaceLuidToGuid</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为接口的 GUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToIndex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85))"><strong>ConvertInterfaceLuidToIndex</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为接口的本地索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85))"><strong>ConvertInterfaceLuidToNameA</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为 ANSI 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85))"><strong>ConvertInterfaceLuidToNameW</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为 Unicode 接口名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85))"><strong>ConvertInterfaceNameToLuidA</strong></a></p></td>
<td align="left"><p>将 ANSI 网络接口名称转换为接口的 LUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85))"><strong>ConvertInterfaceNameToLuidW</strong></a></p></td>
<td align="left"><p>将 Unicode 网络接口名称转换为接口的 LUID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85)" data-raw-source="[&lt;strong&gt;if_indextoname&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85))"><strong>if_indextoname</strong></a></p></td>
<td align="left"><p>将网络接口的本地索引转换为 ANSI 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85)" data-raw-source="[&lt;strong&gt;if_nametoindex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85))"><strong>if_nametoindex</strong></a></p></td>
<td align="left"><p>将网络接口的 ANSI 接口名称转换为接口的本地索引。</p></td>
</tr>
</tbody>
</table>

 

### <a name="interface-management-functions"></a>接口管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552517(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552517(v=vs.85))"><strong>GetIfEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的指定接口的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85))"><strong>GetIfStackTable</strong></a></p></td>
<td align="left"><p>检索网络接口堆栈行条目的表, 这些行条目指定接口堆栈上的网络接口的关系。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"><strong>GetIfTable2</strong></a></p></td>
<td align="left"><p>检索 MIB-II 接口表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2Ex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85))"><strong>GetIfTable2Ex</strong></a></p></td>
<td align="left"><p>检索 MIB-II 接口表, 提供要检索的接口信息级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85)" data-raw-source="[&lt;strong&gt;GetInvertedIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85))"><strong>GetInvertedIfStackTable</strong></a></p></td>
<td align="left"><p>检索反向网络接口堆栈行条目的表, 这些行条目指定接口堆栈上的网络接口的关系。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85))"><strong>GetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的指定接口的 IP 信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85))"><strong>GetIpInterfaceTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 接口条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85))"><strong>InitializeIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>使用默认值初始化<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"><strong>MIB_IPINTERFACE_ROW</strong></a>结构项的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85))"><strong>SetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>设置本地计算机上的 IP 接口的属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-address-management-functions"></a>IP 地址管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546204(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546204(v=vs.85))"><strong>CreateAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上添加新的任意广播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateSortedAddressPairs&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85))"><strong>CreateSortedAddressPairs</strong></a></p></td>
<td align="left"><p>将提供的目标地址列表与主机的本地 IP 地址配对, 并根据首选的通信顺序对对进行排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85))"><strong>CreateUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上添加新的单播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85))"><strong>DeleteAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>删除本地计算机上现有的任意广播 IP 地址条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85))"><strong>DeleteUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>从本地计算机中删除现有的单播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85))"><strong>GetAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上现有的任意广播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"><strong>GetAnycastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的任意播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85))"><strong>GetMulticastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的现有多播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85))"><strong>GetMulticastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的多播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85))"><strong>GetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上现有单播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85))"><strong>GetUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的单播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85))"><strong>InitializeUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>使用本地计算机上的单播 IP 地址条目的默认值初始化<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上稳定的单播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85)" data-raw-source="[&lt;strong&gt;SetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85))"><strong>SetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>设置本地计算机上现有单播 IP 地址条目的属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-neighbor-address-management-functions"></a>IP 邻居地址管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546217(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546217(v=vs.85))"><strong>CreateIpNetEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上创建一个新的邻居 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85))"><strong>DeleteIpNetEntry2</strong></a></p></td>
<td align="left"><p>从本地计算机中删除邻居 IP 地址条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85)" data-raw-source="[&lt;strong&gt;FlushIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85))"><strong>FlushIpNetTable2</strong></a></p></td>
<td align="left"><p>刷新本地计算机上的 IP 邻居表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85))"><strong>GetIpNetEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的邻居 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85))"><strong>GetIpNetTable2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 邻居表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85)" data-raw-source="[&lt;strong&gt;ResolveIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85))"><strong>ResolveIpNetEntry2</strong></a></p></td>
<td align="left"><p>解析本地计算机上的邻居 IP 地址条目的物理地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85))"><strong>SetIpNetEntry2</strong></a></p></td>
<td align="left"><p>设置本地计算机上现有邻居 IP 地址条目的物理地址。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-path-management-functions"></a>IP 路径管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550031(v=vs.85)" data-raw-source="[&lt;strong&gt;FlushIpPathTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550031(v=vs.85))"><strong>FlushIpPathTable</strong></a></p></td>
<td align="left"><p>刷新本地计算机上的 IP 路径表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85))"><strong>GetIpPathEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路径条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85))"><strong>GetIpPathTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路径条目的信息。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-route-management-functions"></a>IP 路由管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546209(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546209(v=vs.85))"><strong>CreateIpForwardEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上创建新的 IP 路由条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85))"><strong>DeleteIpForwardEntry2</strong></a></p></td>
<td align="left"><p>从本地计算机中删除 IP 路由条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85)" data-raw-source="[&lt;strong&gt;GetBestRoute2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85))"><strong>GetBestRoute2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路由条目, 以获得到指定目标 IP 地址的最佳路由。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85))"><strong>GetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路由条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85))"><strong>GetIpForwardTable2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路由条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpForwardEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85))"><strong>InitializeIpForwardEntry</strong></a></p></td>
<td align="left"><p>使用本地计算机上的 IP 路由条目的默认值初始化<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"><strong>MIB_IPFORWARD_ROW2</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85))"><strong>SetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>设置本地计算机上的 IP 路由条目的属性。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-table-memory-management-functions"></a>IP 表内存管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550045(v=vs.85)" data-raw-source="[&lt;strong&gt;FreeMibTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550045(v=vs.85))"><strong>FreeMibTable</strong></a></p></td>
<td align="left"><p>释放返回网络接口、地址和路由 (例如, <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"><strong>GetIfTable2</strong></a>和<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"><strong>GetAnycastIpAddressTable</strong></a>) 的表的函数所分配的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

### <a name="notification-functions"></a>通知函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544864(v=vs.85)" data-raw-source="[&lt;strong&gt;CancelMibChangeNotify2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544864(v=vs.85))"><strong>CancelMibChangeNotify2</strong></a></p></td>
<td align="left"><p>注销用于更改通知的驱动程序, 以便进行 IP 接口更改、IP 地址更改、IP 路由更改和检索稳定的单播 IP 地址表的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyIpInterfaceChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))"><strong>NotifyIpInterfaceChange</strong></a></p></td>
<td align="left"><p>注册驱动程序, 以便在本地计算机上的所有 IP 接口、IPv4 接口或 IPv6 接口发生更改时获得通知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyRouteChange2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85))"><strong>NotifyRouteChange2</strong></a></p></td>
<td align="left"><p>注册, 通知本地计算机上 IP 路由项的更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyUnicastIpAddressChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85))"><strong>NotifyUnicastIpAddressChange</strong></a></p></td>
<td align="left"><p>将通知注册到本地计算机上所有单播 IP 接口、单播 IPv4 地址或单播 IPv6 地址的更改。</p></td>
</tr>
</tbody>
</table>

 

### <a name="teredo-ipv6-client-management-functions"></a>Teredo IPv6 客户端管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">才能</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552578(v=vs.85)" data-raw-source="[&lt;strong&gt;GetTeredoPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552578(v=vs.85))"><strong>GetTeredoPort</strong></a></p></td>
<td align="left"><p>检索 Teredo 客户端在本地计算机上使用的动态 UDP 端口号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyTeredoPortChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85))"><strong>NotifyTeredoPortChange</strong></a></p></td>
<td align="left"><p>注册, 通知对 Teredo 客户端为本地计算机上的 Teredo 服务端口所使用的 UDP 端口号进行了更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上稳定的单播 IP 地址表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mib-structures"></a>MIB 结构

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">构造</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557013(v=vs.85)" data-raw-source="[&lt;strong&gt;IP_ADDRESS_PREFIX&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557013(v=vs.85))"><strong>IP_ADDRESS_PREFIX</strong></a></p></td>
<td align="left"><p>存储 IP 地址前缀。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储有关任意播 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>包含一个包含任意播 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85))"><strong>MIB_IF_ROW2</strong></a></p></td>
<td align="left"><p>存储有关特定接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85))"><strong>MIB_IF_TABLE2</strong></a></p></td>
<td align="left"><p>包含一个逻辑和物理接口项的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85))"><strong>MIB_IFSTACK_ROW</strong></a></p></td>
<td align="left"><p>表示两个网络接口之间的关系。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85))"><strong>MIB_IFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>包含网络接口堆栈中的行项的表。 此表指定接口堆栈上的网络接口的关系。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_ROW</strong></a></p></td>
<td align="left"><p>表示两个网络接口之间的关系。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>包含一个反转网络接口堆栈行项的表。 此表以相反顺序指定了接口堆栈上的网络接口的关系。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"><strong>MIB_IPFORWARD_ROW2</strong></a></p></td>
<td align="left"><p>存储有关 IP 路由条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85))"><strong>MIB_IPFORWARD_TABLE2</strong></a></p></td>
<td align="left"><p>包含一个 IP 路由条目表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"><strong>MIB_IPINTERFACE_ROW</strong></a></p></td>
<td align="left"><p>为网络接口上的特定 IP 地址系列存储接口管理信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85))"><strong>MIB_IPINTERFACE_TABLE</strong></a></p></td>
<td align="left"><p>包含一个 IP 接口条目表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85))"><strong>MIB_IPNET_ROW2</strong></a></p></td>
<td align="left"><p>存储有关邻居 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85))"><strong>MIB_IPNET_TABLE2</strong></a></p></td>
<td align="left"><p>包含邻居 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85))"><strong>MIB_IPPATH_ROW</strong></a></p></td>
<td align="left"><p>存储有关 IP 路径条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85))"><strong>MIB_IPPATH_TABLE</strong></a></p></td>
<td align="left"><p>包含 IP 路径项的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储有关多播 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>包含多播 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储有关单播 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>包含单播 IP 地址条目的表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mib-enumerations"></a>MIB 枚举

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">枚举</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/netioapi/ne-netioapi-_mib_if_table_level" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE_LEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/netioapi/ne-netioapi-_mib_if_table_level)"><strong>MIB_IF_TABLE_LEVEL</strong></a></p></td>
<td align="left"><p>定义要检索的接口信息的级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_NOTIFICATION_TYPE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85))"><strong>MIB_NOTIFICATION_TYPE</strong></a></p></td>
<td align="left"><p>定义当发生通知时传递给回调函数的通知类型。</p></td>
</tr>
</tbody>
</table>

 

### <a name="nl-enumerations"></a>NL 枚举

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">枚举</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_address_type" data-raw-source="[&lt;strong&gt;NL_ADDRESS_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_address_type)"><strong>NL_ADDRESS_TYPE</strong></a></p></td>
<td align="left"><p>指定网络层的 IP 地址类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568758(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_DAD_STATE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568758(v=vs.85))"><strong>NL_DAD_STATE</strong></a></p></td>
<td align="left"><p>定义重复地址检测 (DAD) 状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior" data-raw-source="[&lt;strong&gt;NL_LINK_LOCAL_ADDRESS_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior)"><strong>NL_LINK_LOCAL_ADDRESS_BEHAVIOR</strong></a></p></td>
<td align="left"><p>定义链接本地地址行为。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state" data-raw-source="[&lt;strong&gt;NL_NEIGHBOR_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state)"><strong>NL_NEIGHBOR_STATE</strong></a></p></td>
<td align="left"><p>定义网络层邻域 IP 地址的状态, 如 RFC 2461 中所述的7.3.2 部分中所述。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_PREFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85))"><strong>NL_PREFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 地址的前缀或网络部分的源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin" data-raw-source="[&lt;strong&gt;NL_ROUTE_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin)"><strong>NL_ROUTE_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 路由的源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol" data-raw-source="[&lt;strong&gt;NL_ROUTE_PROTOCOL&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol)"><strong>NL_ROUTE_PROTOCOL</strong></a></p></td>
<td align="left"><p>定义将 IP 路由添加到的路由机制, 如 RFC 4292 中所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior" data-raw-source="[&lt;strong&gt;NL_ROUTER_DISCOVERY_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior)"><strong>NL_ROUTER_DISCOVERY_BEHAVIOR</strong></a></p></td>
<td align="left"><p>定义路由器发现行为, 如 RFC 2461 中所述。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_SUFFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85))"><strong>NL_SUFFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 地址的后缀或主机部分的源。</p></td>
</tr>
</tbody>
</table>

 

 

 





