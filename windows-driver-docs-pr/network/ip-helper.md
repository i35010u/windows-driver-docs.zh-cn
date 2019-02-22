---
title: IP 帮助程序
description: IP 帮助程序
ms.assetid: c7cf1f47-ee0d-4c89-883b-717b719fcc2a
keywords:
- IP 帮助程序 WDK 网络
- 网络、 大约 IP 帮助程序 WDK
- 网络驱动程序 WDK，IP 帮助程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7d3f15c108b21edfe9ecd8763d4211f5709fd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544431"
---
# <a name="ip-helper"></a>IP 帮助程序





Internet 协议帮助程序 （IP 帮助程序） 使驱动程序检索有关本地计算机的网络配置的信息以及如何修改该配置。 IP 帮助程序还提供了通知机制，以确保在本地计算机的某些方面的网络配置更改时，会通知驱动程序。 IP 帮助程序是在 Windows Vista 和更高版本的 Microsoft Windows 操作系统中可用。

许多 IP 帮助程序函数将表示的管理信息基础 (MIB) 技术与相关联的数据类型的结构参数传递。 IP 帮助程序函数使用这些 MIB 结构来表示网络的各种信息。

IP 帮助程序文档使用术语"适配器"和"接口"广泛。 *适配器*是一种的缩写的形式的旧字词*网络适配器*，其最初称为某种形式的网络硬件。 适配器是数据保持链接级抽象。

*接口*IETF RFC 文档中称为一个抽象的概念，表示为链接的节点的附件。 接口是 IP 级抽象。

您的驱动程序可以使用以下内核模式函数、 MIB 结构和 MIB 和网络层 (NL) 枚举来检索和修改本地计算机上的传输控制协议 /internet 协议 (TCP/IP) 传输的配置设置。

**请注意**  开发驱动程序代码时, 按照说明[包括标头文件。](including-header-files-for-ip-helper.md)

 

### <a name="interface-conversion-functions"></a>接口转换函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546130" data-raw-source="[&lt;strong&gt;ConvertInterfaceAliasToLuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546130)"><strong>ConvertInterfaceAliasToLuid</strong></a></p></td>
<td align="left"><p>将本地唯一标识符 (LUID) 转换为网络接口到 Unicode 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546137" data-raw-source="[&lt;strong&gt;ConvertInterfaceGuidToLuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546137)"><strong>ConvertInterfaceGuidToLuid</strong></a></p></td>
<td align="left"><p>将全局唯一标识符 (GUID) 转换为网络接口到接口的 LUID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546141" data-raw-source="[&lt;strong&gt;ConvertInterfaceIndexToLuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546141)"><strong>ConvertInterfaceIndexToLuid</strong></a></p></td>
<td align="left"><p>将网络接口的一个本地索引转换为接口的 LUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546151" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToAlias&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546151)"><strong>ConvertInterfaceLuidToAlias</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为接口别名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546156" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546156)"><strong>ConvertInterfaceLuidToGuid</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为接口的 GUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546167" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546167)"><strong>ConvertInterfaceLuidToIndex</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为本地的接口索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546171" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546171)"><strong>ConvertInterfaceLuidToNameA</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为 ANSI 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546175" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546175)"><strong>ConvertInterfaceLuidToNameW</strong></a></p></td>
<td align="left"><p>将网络接口的 LUID 转换为 Unicode 接口名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546185" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546185)"><strong>ConvertInterfaceNameToLuidA</strong></a></p></td>
<td align="left"><p>将 ANSI 网络接口名称转换为接口的 LUID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546192" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546192)"><strong>ConvertInterfaceNameToLuidW</strong></a></p></td>
<td align="left"><p>将 Unicode 网络接口名称转换为接口的 LUID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553785" data-raw-source="[&lt;strong&gt;if_indextoname&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553785)"><strong>if_indextoname</strong></a></p></td>
<td align="left"><p>将本地网络接口的索引转换为 ANSI 接口名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553788" data-raw-source="[&lt;strong&gt;if_nametoindex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553788)"><strong>if_nametoindex</strong></a></p></td>
<td align="left"><p>将网络接口的 ANSI 界面名称转换为本地的接口索引。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552517" data-raw-source="[&lt;strong&gt;GetIfEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552517)"><strong>GetIfEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的指定接口的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552521" data-raw-source="[&lt;strong&gt;GetIfStackTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552521)"><strong>GetIfStackTable</strong></a></p></td>
<td align="left"><p>检索的网络接口堆栈行项的接口堆栈上指定的网络接口的关系的表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552524" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552524)"><strong>GetIfTable2</strong></a></p></td>
<td align="left"><p>检索 MIB-II 接口表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552528" data-raw-source="[&lt;strong&gt;GetIfTable2Ex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552528)"><strong>GetIfTable2Ex</strong></a></p></td>
<td align="left"><p>检索 MIB-II 接口表，提供的接口检索信息的级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552531" data-raw-source="[&lt;strong&gt;GetInvertedIfStackTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552531)"><strong>GetInvertedIfStackTable</strong></a></p></td>
<td align="left"><p>检索的倒排的网络接口堆栈行项的接口堆栈上指定的网络接口的关系的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552540" data-raw-source="[&lt;strong&gt;GetIpInterfaceEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552540)"><strong>GetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的指定接口的 IP 信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552543" data-raw-source="[&lt;strong&gt;GetIpInterfaceTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552543)"><strong>GetIpInterfaceTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 接口项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554883" data-raw-source="[&lt;strong&gt;InitializeIpInterfaceEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554883)"><strong>InitializeIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>初始化的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff559254" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559254)"> <strong>MIB_IPINTERFACE_ROW</strong> </a>结构使用默认值的条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570774" data-raw-source="[&lt;strong&gt;SetIpInterfaceEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570774)"><strong>SetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上设置 IP 接口的属性。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546204" data-raw-source="[&lt;strong&gt;CreateAnycastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546204)"><strong>CreateAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上添加新的任意广播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546219" data-raw-source="[&lt;strong&gt;CreateSortedAddressPairs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546219)"><strong>CreateSortedAddressPairs</strong></a></p></td>
<td align="left"><p>对提供的主机以及目标地址列表&#39;s 本地 IP 地址，对根据通信的首选顺序对进行排序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546227" data-raw-source="[&lt;strong&gt;CreateUnicastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546227)"><strong>CreateUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上添加新的单播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546363" data-raw-source="[&lt;strong&gt;DeleteAnycastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546363)"><strong>DeleteAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>删除本地计算机上的现有任意广播 IP 地址条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546370" data-raw-source="[&lt;strong&gt;DeleteUnicastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546370)"><strong>DeleteUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>从本地计算机中删除一个现有的单播 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552504" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552504)"><strong>GetAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的某个现有的任意广播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552508" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552508)"><strong>GetAnycastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的任意广播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552565" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552565)"><strong>GetMulticastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的某个现有的多播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552570" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552570)"><strong>GetMulticastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的多播的 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552589" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552589)"><strong>GetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的某个现有的单播 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552594" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552594)"><strong>GetUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上的单播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554886" data-raw-source="[&lt;strong&gt;InitializeUnicastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554886)"><strong>InitializeUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>初始化<a href="https://msdn.microsoft.com/library/windows/hardware/ff559308" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559308)"> <strong>MIB_UNICASTIPADDRESS_ROW</strong> </a>结构使用的本地计算机上的单播 IP 地址项默认值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568807" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568807)"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>检索本地计算机上稳定的单播 IP 地址表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570800" data-raw-source="[&lt;strong&gt;SetUnicastIpAddressEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570800)"><strong>SetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>在本地计算机上设置的一个现有的单播 IP 地址条目的属性。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546217" data-raw-source="[&lt;strong&gt;CreateIpNetEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546217)"><strong>CreateIpNetEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上创建一个新的邻居 IP 地址条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546368" data-raw-source="[&lt;strong&gt;DeleteIpNetEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546368)"><strong>DeleteIpNetEntry2</strong></a></p></td>
<td align="left"><p>从本地计算机中删除邻居 IP 地址条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550029" data-raw-source="[&lt;strong&gt;FlushIpNetTable2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550029)"><strong>FlushIpNetTable2</strong></a></p></td>
<td align="left"><p>刷新本地计算机上的 IP 邻居表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552546" data-raw-source="[&lt;strong&gt;GetIpNetEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552546)"><strong>GetIpNetEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的邻居 IP 地址条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552551" data-raw-source="[&lt;strong&gt;GetIpNetTable2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552551)"><strong>GetIpNetTable2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 邻居表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570686" data-raw-source="[&lt;strong&gt;ResolveIpNetEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570686)"><strong>ResolveIpNetEntry2</strong></a></p></td>
<td align="left"><p>解析本地计算机上一个邻居 IP 地址条目的物理地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570775" data-raw-source="[&lt;strong&gt;SetIpNetEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570775)"><strong>SetIpNetEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上设置现有邻居 IP 地址条目的物理的地址。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550031" data-raw-source="[&lt;strong&gt;FlushIpPathTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550031)"><strong>FlushIpPathTable</strong></a></p></td>
<td align="left"><p>刷新本地计算机上的 IP 路径表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552556" data-raw-source="[&lt;strong&gt;GetIpPathEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552556)"><strong>GetIpPathEntry</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路径条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552559" data-raw-source="[&lt;strong&gt;GetIpPathTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552559)"><strong>GetIpPathTable</strong></a></p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546209" data-raw-source="[&lt;strong&gt;CreateIpForwardEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546209)"><strong>CreateIpForwardEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上创建一个新的 IP 路由条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546365" data-raw-source="[&lt;strong&gt;DeleteIpForwardEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546365)"><strong>DeleteIpForwardEntry2</strong></a></p></td>
<td align="left"><p>从本地计算机中删除 IP 路由项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552511" data-raw-source="[&lt;strong&gt;GetBestRoute2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552511)"><strong>GetBestRoute2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的最佳路由到指定的目标 IP 地址上的 IP 路由条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552535" data-raw-source="[&lt;strong&gt;GetIpForwardEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552535)"><strong>GetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路由条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552536" data-raw-source="[&lt;strong&gt;GetIpForwardTable2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552536)"><strong>GetIpForwardTable2</strong></a></p></td>
<td align="left"><p>检索本地计算机上的 IP 路由条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554882" data-raw-source="[&lt;strong&gt;InitializeIpForwardEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554882)"><strong>InitializeIpForwardEntry</strong></a></p></td>
<td align="left"><p>初始化<a href="https://msdn.microsoft.com/library/windows/hardware/ff559245" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559245)"> <strong>MIB_IPFORWARD_ROW2</strong> </a>使用本地计算机上的 IP 路由条目的默认值的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570773" data-raw-source="[&lt;strong&gt;SetIpForwardEntry2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570773)"><strong>SetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>在本地计算机上设置的 IP 路由条目的属性。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550045" data-raw-source="[&lt;strong&gt;FreeMibTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550045)"><strong>FreeMibTable</strong></a></p></td>
<td align="left"><p>释放由返回的网络接口、 地址和路由表的函数分配的缓冲区 (例如， <a href="https://msdn.microsoft.com/library/windows/hardware/ff552524" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552524)"> <strong>GetIfTable2</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff552508" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552508)"> <strong>GetAnycastIpAddressTable</strong></a>)。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544864" data-raw-source="[&lt;strong&gt;CancelMibChangeNotify2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544864)"><strong>CancelMibChangeNotify2</strong></a></p></td>
<td align="left"><p>注销的 IP 接口更改、 IP 地址更改、 IP 路由更改和进行请求以便检索稳定的单播 IP 地址表更改通知的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568805" data-raw-source="[&lt;strong&gt;NotifyIpInterfaceChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568805)"><strong>NotifyIpInterfaceChange</strong></a></p></td>
<td align="left"><p>注册以获得对所有 IP 接口、 IPv4 接口或在本地计算机上的 IPv6 接口的更改的通知的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568806" data-raw-source="[&lt;strong&gt;NotifyRouteChange2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568806)"><strong>NotifyRouteChange2</strong></a></p></td>
<td align="left"><p>注册以获得对本地计算机上的 IP 路由条目的更改的通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568809" data-raw-source="[&lt;strong&gt;NotifyUnicastIpAddressChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568809)"><strong>NotifyUnicastIpAddressChange</strong></a></p></td>
<td align="left"><p>注册以获得对所有单播 IP 接口、 的单播 IPv4 地址或在本地计算机上的单播 IPv6 地址的更改的通知。</p></td>
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
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552578" data-raw-source="[&lt;strong&gt;GetTeredoPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552578)"><strong>GetTeredoPort</strong></a></p></td>
<td align="left"><p>检索本地计算机的 Teredo 客户端使用的动态 UDP 端口号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568808" data-raw-source="[&lt;strong&gt;NotifyTeredoPortChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568808)"><strong>NotifyTeredoPortChange</strong></a></p></td>
<td align="left"><p>注册以获得对 Teredo 客户端使用本地计算机上的 Teredo 服务端口的 UDP 端口号的更改的通知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568807" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568807)"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
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
<th align="left">结构</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557013" data-raw-source="[&lt;strong&gt;IP_ADDRESS_PREFIX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557013)"><strong>IP_ADDRESS_PREFIX</strong></a></p></td>
<td align="left"><p>将存储 IP 地址前缀。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559190" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559190)"><strong>MIB_ANYCASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储任意广播 IP 地址的相关信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559193" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559193)"><strong>MIB_ANYCASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>包含任意广播 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559214" data-raw-source="[&lt;strong&gt;MIB_IF_ROW2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559214)"><strong>MIB_IF_ROW2</strong></a></p></td>
<td align="left"><p>存储有关某个特定接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559224" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559224)"><strong>MIB_IF_TABLE2</strong></a></p></td>
<td align="left"><p>包含逻辑和物理接口条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559207" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559207)"><strong>MIB_IFSTACK_ROW</strong></a></p></td>
<td align="left"><p>表示两个网络接口之间的关系。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559210" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559210)"><strong>MIB_IFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>包含网络接口堆栈中的行项的表。 此表接口堆栈上指定的网络接口的关系。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559234" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559234)"><strong>MIB_INVERTEDIFSTACK_ROW</strong></a></p></td>
<td align="left"><p>表示两个网络接口之间的关系。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559240" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559240)"><strong>MIB_INVERTEDIFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>包含倒排的网络接口堆栈行条目的表。 此表按相反的顺序指定接口堆栈上的网络接口的关系。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559245" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559245)"><strong>MIB_IPFORWARD_ROW2</strong></a></p></td>
<td align="left"><p>存储有关 IP 路由条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559252" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_TABLE2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559252)"><strong>MIB_IPFORWARD_TABLE2</strong></a></p></td>
<td align="left"><p>包含 IP 路由项的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559254" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559254)"><strong>MIB_IPINTERFACE_ROW</strong></a></p></td>
<td align="left"><p>存储的接口为特定的 IP 地址族的网络接口上的管理信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559260" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559260)"><strong>MIB_IPINTERFACE_TABLE</strong></a></p></td>
<td align="left"><p>包含接口的 IP 项的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559263" data-raw-source="[&lt;strong&gt;MIB_IPNET_ROW2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559263)"><strong>MIB_IPNET_ROW2</strong></a></p></td>
<td align="left"><p>存储有关邻居 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559267" data-raw-source="[&lt;strong&gt;MIB_IPNET_TABLE2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559267)"><strong>MIB_IPNET_TABLE2</strong></a></p></td>
<td align="left"><p>包含邻居 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559270" data-raw-source="[&lt;strong&gt;MIB_IPPATH_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559270)"><strong>MIB_IPPATH_ROW</strong></a></p></td>
<td align="left"><p>存储有关 IP 路径条目的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559273" data-raw-source="[&lt;strong&gt;MIB_IPPATH_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559273)"><strong>MIB_IPPATH_TABLE</strong></a></p></td>
<td align="left"><p>包含 IP 路径项的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559277" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559277)"><strong>MIB_MULTICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储有关多播的 IP 地址的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559281" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559281)"><strong>MIB_MULTICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>包含多播 IP 地址条目的表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559308" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559308)"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>存储信息的单播 IP 地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559322" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559322)"><strong>MIB_UNICASTIPADDRESS_TABLE</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559229" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE_LEVEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559229)"><strong>MIB_IF_TABLE_LEVEL</strong></a></p></td>
<td align="left"><p>定义要检索的接口信息的级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559286" data-raw-source="[&lt;strong&gt;MIB_NOTIFICATION_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559286)"><strong>MIB_NOTIFICATION_TYPE</strong></a></p></td>
<td align="left"><p>定义时出现通知传递给回调函数的通知类型。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568757" data-raw-source="[&lt;strong&gt;NL_ADDRESS_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568757)"><strong>NL_ADDRESS_TYPE</strong></a></p></td>
<td align="left"><p>指定网络层的 IP 地址的类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568758" data-raw-source="[&lt;strong&gt;NL_DAD_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568758)"><strong>NL_DAD_STATE</strong></a></p></td>
<td align="left"><p>定义重复地址检测 (DAD) 状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568760" data-raw-source="[&lt;strong&gt;NL_LINK_LOCAL_ADDRESS_BEHAVIOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568760)"><strong>NL_LINK_LOCAL_ADDRESS_BEHAVIOR</strong></a></p></td>
<td align="left"><p>定义链接本地地址行为。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568761" data-raw-source="[&lt;strong&gt;NL_NEIGHBOR_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568761)"><strong>NL_NEIGHBOR_STATE</strong></a></p></td>
<td align="left"><p>RFC 2461，部分 7.3.2 中所述定义的网络层邻居 IP 地址的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568762" data-raw-source="[&lt;strong&gt;NL_PREFIX_ORIGIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568762)"><strong>NL_PREFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 地址的前缀或网络一部分的原点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568764" data-raw-source="[&lt;strong&gt;NL_ROUTE_ORIGIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568764)"><strong>NL_ROUTE_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 路由的源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568766" data-raw-source="[&lt;strong&gt;NL_ROUTE_PROTOCOL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568766)"><strong>NL_ROUTE_PROTOCOL</strong></a></p></td>
<td align="left"><p>定义与，已添加的 IP 路由的路由机制，如 RFC 4292 中所述。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568763" data-raw-source="[&lt;strong&gt;NL_ROUTER_DISCOVERY_BEHAVIOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568763)"><strong>NL_ROUTER_DISCOVERY_BEHAVIOR</strong></a></p></td>
<td align="left"><p>定义路由器发现行为，如 RFC 2461 中所述。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568768" data-raw-source="[&lt;strong&gt;NL_SUFFIX_ORIGIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568768)"><strong>NL_SUFFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>定义 IP 地址的后缀或主机一部分的原点。</p></td>
</tr>
</tbody>
</table>

 

 

 





