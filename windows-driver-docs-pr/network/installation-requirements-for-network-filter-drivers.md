---
title: 网络筛选器驱动程序的安装要求
description: 网络筛选器驱动程序的安装要求
ms.assetid: 7fb31e18-a2f0-48fe-b0a8-cf4aca7d27d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9288d57545388f760608e47a8e9eb367a08d695
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207907"
---
# <a name="installation-requirements-for-network-filter-drivers"></a>网络筛选器驱动程序的安装要求





本主题概述网络筛选器驱动程序的 INF 文件要求。 在 NDIS 6.0 和更高版本中支持筛选器驱动程序。 有关如何安装筛选器驱动程序的详细信息，请参阅 " [NDIS 筛选器驱动程序安装](ndis-filter-driver-installation.md)"。

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
<td align="left"><p></p>
<strong>类</strong>= 空间 <strong>ClassGuid</strong>= {4D36E974-E325-11CE-BFC1-08002BE10318}</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](../install/inf-sourcedisksnames-section.md)"><strong>Inf SourceDisksNames 部分</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](../install/inf-sourcedisksfiles-section.md)"> <strong>inf SourceDisksFiles 部分</strong></a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](../install/inf-destinationdirs-section.md)"><strong>INF DestinationDirs 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](../install/inf-manufacturer-section.md)"><strong>INF Manufacturer 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">模型部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><em>Hw id</em>应该包含提供程序名称，后跟下划线和制造商名称或产品名称 (例如 MS_DLC) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><strong>特征</strong> 条目：</p>
<p>NCF_LW_FILTER 设置 (0x40000) 。 筛选器驱动程序不得将 NCF_FILTER (0x400) 标志。 NCF_<em>Xxx</em> 标志的值是在 Netcfgx 中定义的。 有关 NCF_<em>Xxx</em> 标志的详细信息，请参阅 <a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section in a Network INF File](ddinstall-section-in-a-network-inf-file.md)">网络 INF 文件中的 DDInstall 部分</a>。</p>
<p>设置 <strong>NetCfgInstanceId</strong> 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">添加-注册表-部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>创建 Ndi 键</p>
<p>INF 文件的 "<strong>服务安装</strong>" 部分中的<strong>ServiceBinary</strong>条目指定筛选器驱动程序的二进制文件的路径。</p>
<p>设置 " <strong>FilterType</strong> " 和 " <strong>FilterRunType</strong> "。 请参阅 <a href="types-of-filter-drivers.md" data-raw-source="[Types of Filter Drivers](types-of-filter-drivers.md)">筛选器驱动程序的类型</a>。</p>
<p>设置 <strong>UpperRange</strong>、 <strong>LowerRange</strong>和 <strong>FilterMediaTypes</strong> 条目。 请参阅 <a href="specifying-filter-driver-binding-relationships.md" data-raw-source="[Specifying Filter Driver Binding Relationships](specifying-filter-driver-binding-relationships.md)">指定筛选器驱动程序绑定关系</a>。</p>
<p>为 <strong>CoServices</strong> 属性指定筛选器的主服务名称。</p>
<p>指定 <strong>FilterClass</strong> 以确定修改筛选器的堆栈中的顺序。 请参阅 <a href="configuring-an-inf-file-for-a-modifying-filter-driver.md" data-raw-source="[Configuring an INF File for a Modifying Filter Driver](configuring-an-inf-file-for-a-modifying-filter-driver.md)">配置用于修改筛选器驱动程序的 INF 文件</a>。</p>
<p>另请参阅<a href="configuring-an-inf-file-for-a-monitoring-filter-driver.md" data-raw-source="[Configuring an INF File for a Monitoring Filter Driver](configuring-an-inf-file-for-a-monitoring-filter-driver.md)">配置监视筛选器驱动程序的 INF 文件</a>、<a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Adding Service-Related Values to the Ndi Key](adding-service-related-values-to-the-ndi-key.md)">将与服务相关的值添加到</a><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section in a Network INF File](ddinstall-services-section-in-a-network-inf-file.md)">网络 INF 文件中</a>的 Ndi 键和 DDInstall 部分。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">为组件设置静态参数</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">要求安装另一个网络组件</a></p>
<p><a href="adding-a-helptext-value.md" data-raw-source="[Adding a HelpText Value](adding-a-helptext-value.md)">添加 HelpText 值</a></p>
<p><a href="adding-registry-values-for-a-notify-object.md" data-raw-source="[Adding Registry Values for a Notify Object](adding-registry-values-for-a-notify-object.md)">添加通知对象的注册表值</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="remove-section-in-a-network-inf-file.md" data-raw-source="[Remove Section](remove-section-in-a-network-inf-file.md)">删除节</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](../install/inf-strings-section.md)"><strong>INF Strings 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
</tbody>
</table>

 

 

