---
title: 网络适配器的安装要求
description: 网络适配器的安装要求
ms.assetid: 682a262a-a712-4fab-a753-d0c6fc08bac8
keywords:
- 网络适配器安装要求 WDK
- 适配器 WDK 网络，安装要求
- WAN WDK 网络，适配器安装要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18521d53edec3da03513c7089887f91163d867d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218091"
---
# <a name="installation-requirements-for-network-adapters"></a>网络适配器的安装要求





本主题概述网络适配器的安装要求。

**注意**   NDIS 6.0 和更高版本的驱动程序支持一组[用于网络设备的标准 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

### <a name="general-requirements"></a>一般要求

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件部分</th>
<th align="left">状态</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="version-section-in-a-network-inf-file.md" data-raw-source="[Version Section](version-section-in-a-network-inf-file.md)">版本部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><strong>类</strong>= Net</p>
<p><strong>ClassGuid</strong>= {4D36E972-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](../install/inf-sourcedisksnames-section.md)"><strong>Inf SourceDisksNames 部分</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](../install/inf-sourcedisksfiles-section.md)"> <strong>inf SourceDisksFiles 部分</strong></a></p></td>
<td align="left"><p>必需的 if .。。</p></td>
<td align="left"><p>如果 INF 文件未与 Windows 2000 一起分发，则是必需的。 如果 INF 文件与 Windows 2000 一起分发，则必须在 "<strong>版本</strong>" 部分中指定<strong>LayoutFile</strong>项，并且不会使用<strong>SourceDisksNames</strong>和<strong>SourceDisksFiles</strong>部分。</p>
<p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](../install/inf-destinationdirs-section.md)"><strong>INF DestinationDirs 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags 部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>必须包含由 INF 文件安装的每个即插即用 (PnP) 适配器的 <strong>ExcludeFromSelect</strong> 项。</p>
<p>不应列出非 PnP 适配器，如非 PnP ISA 和 EISA 适配器。 请注意，Windows XP 和更高版本的操作系统不支持非 PnP ISA 适配器和 EISA 适配器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](../install/inf-manufacturer-section.md)"><strong>INF Manufacturer 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">模型部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><em>Hw id</em>必须与适配器提供给 PnP 管理器的硬件 id 匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><strong>特征</strong> 条目</p>
<p>允许的值：</p>
<p>NCF_VIRTUAL，</p>
<p>NCF_SOFTWARE_ENUMERATED、NCF_PHYSICAL、NCF_MULTIPORT_INSTANCED_ADAPTER、NCF_HAS_UI、NCF_HIDDEN、NCF_NOT_USER_REMOVABLE</p>
<p>NCF_VIRTUAL、NCF_SOFTWARE_ENUMERATED 和 NCF_PHYSICAL 互相排斥。</p>
<p>物理适配器需要 <strong>BusType</strong> 条目。</p>
<p>EISA 适配器需要 <strong>EisaCompressedId</strong> 条目。 此条目为适配器指定 EISA 压缩 ID 和适配器掩码。 Windows XP 和更高版本的操作系统不支持 EISA 适配器。</p>
<p>多端口网络适配器需要 <strong>Port1DeviceNumber</strong> 或 <strong>Port1FunctionNumber</strong> 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">添加-注册表-部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>创建 Ndi 键</p>
<p><a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Specifying service-related values](adding-service-related-values-to-the-ndi-key.md)">指定服务相关值</a></p>
<p>仅为 LBFO 微型端口驱动程序<a href="specifying-bundle-membership.md" data-raw-source="[Specifying Bundle Membership](specifying-bundle-membership.md)">指定绑定成员身份</a> () </p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">指定绑定接口</a></p>
<p>允许的绑定接口：</p>
<p><strong>UpperRange</strong>：</p>
<p>ndis5、ndisatm、ndiswan、ndiscowan、noupper、ndis5_atalk、ndis5_dlc、ndis5_ip、ndis5_ipx、ndis5_nbf、ndis5_streams</p>
<p><strong>LowerRange</strong>：</p>
<p>以太网，atm，tokenring，串行，fddi，基带，宽带，arcnet，isdn，localtalk，wan</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">为组件设置静态参数</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">要求安装另一个网络组件</a></p>
<p><a href="specifying-configuration-parameters-for-the-advanced-properties-page.md" data-raw-source="[Specifying Configuration Parameters for the Advanced Properties Page](specifying-configuration-parameters-for-the-advanced-properties-page.md)">指定高级属性页的配置参数</a></p>
<p><a href="specifying-custom-property-pages-for-network-adapters.md" data-raw-source="[Specifying Custom Property Pages for Network Adapters](specifying-custom-property-pages-for-network-adapters.md)">指定网络适配器的自定义属性页</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](../install/inf-strings-section.md)"><strong>INF Strings 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
</tbody>
</table>

 

### <a name="additional-requirements-for-wan-adapters"></a>WAN 适配器的其他要求

WAN 适配器具有以下主题中所述的其他安装要求：

[指定 WAN 适配器的 WAN 终结点](specifying-wan-endpoints-for-a-wan-adapter.md)

[指定 ISDN 适配器的 ISDN 键和值](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)

[安装多协议 WAN NIC](installing-a-multiprotocol-wan-nic.md)

**注意**   不支持[删除部分](remove-section-in-a-network-inf-file.md)和[网络组件的通知对象](notify-objects-for-network-components.md)。

 

 

