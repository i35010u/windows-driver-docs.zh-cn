---
title: 网络筛选器中间驱动程序的安装要求
description: 网络筛选器中间驱动程序的安装要求
ms.assetid: 17eb9045-1466-4bd2-8805-964d339c4a9f
keywords:
- 网络筛选器的中间驱动程序安装要求 WDK
- 服务 INF 文件 WDK 网络
- 设备 INF 文件 WDK 联网
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb2120ab5820a3dda8c29c3f6c5fe65bcf6151c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393359"
---
# <a name="installation-requirements-for-network-filter-intermediate-drivers"></a>网络筛选器中间驱动程序的安装要求





**请注意**  NDIS 6.0 及更高版本不支持筛选器中间驱动程序。 应改为使用 NDIS 筛选器驱动程序接口。 NDIS 筛选器驱动程序有关的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers.md)。

 

本主题总结了 NDIS 5 的 INF 文件要求。*x*网络筛选器中间驱动程序。

安装网络筛选器中间驱动程序需要两个 INF 文件：

-   驱动程序服务 (**类**= NetService)

-   设备驱动程序 (**类**= Net)

### <a name="service-inf-file-for-a-network-filter-intermediate-driver"></a>服务网络筛选器中间驱动程序的 INF 文件

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
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="version-section-in-a-network-inf-file.md" data-raw-source="[Version Section](version-section-in-a-network-inf-file.md)">版本部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><strong>类</strong>= NetService</p>
<p><strong>ClassGuid</strong>= {4D36E974-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)"><strong>INF SourceDisksNames 部分</strong></a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)"> <strong>INF SourceDisksFiles 部分</strong></a></p></td>
<td align="left"><p>如果使用...</p></td>
<td align="left"><p>所需如果 INF 文件不随 Windows 2000。 如果 INF 文件随 Windows 2000 <strong>LayoutFile</strong>必须在指定项<strong>版本</strong>部分中，并<strong>SourceDisksNames</strong>和<strong>SourceDisksFiles</strong>未使用部分。</p>
<p>没有特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)"><strong>INF DestinationDirs 部分</strong></a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)"><strong>INF 制造商部分</strong></a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">模型部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><em>Hw id</em>应包含下划线后跟提供程序名称和制造商名称或产品名称-例如：MS_DLC.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><strong>特征</strong>条目：</p>
<p>NCF_FILTER 是必需的。 NCF_HAS_UI 和 NCF_NO_SERVICE 是可选的。</p>
<p>设备 INF 必须复制到系统 INF 目录中，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files" data-raw-source="[Copying INFs](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)">复制 Inf</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall.Services 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">Add-registry-sections</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>创建 Ndi 密钥</p>
<p>FilterClass，FilterDeviceInfId，FilterMediaTypes</p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">指定绑定接口</a></p>
<p>允许的绑定接口：</p>
<p>UpperRange: noupper</p>
<p>LowerRange: nolower</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">设置组件的静态参数</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">需安装另一个网络组件</a></p>
<p><a href="adding-a-helptext-value.md" data-raw-source="[Adding a HelpText Value](adding-a-helptext-value.md)">添加 HelpText 值</a></p>
<p><a href="adding-registry-values-for-a-notify-object.md" data-raw-source="[Adding Registry Values for a Notify Object](adding-registry-values-for-a-notify-object.md)">将注册表值添加通知对象</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="remove-section-in-a-network-inf-file.md" data-raw-source="[Remove Section](remove-section-in-a-network-inf-file.md)">删除节</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)"><strong>INF 字符串部分</strong></a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-inf-file-for-a-network-filter-intermediate-driver"></a>设备网络筛选器中间驱动程序的 INF 文件

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
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="version-section-in-a-network-inf-file.md" data-raw-source="[Version Section](version-section-in-a-network-inf-file.md)">版本部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><strong>类</strong>= Net</p>
<p><strong>ClassGuid</strong>= {4D36E972-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags 部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>本部分必须包含<strong>ExcludeFromSelect</strong>的设备条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)"><strong>INF 制造商部分</strong></a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">模型部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><em>Hw id</em>应包含下划线后跟提供程序名称和制造商名称或产品名称-例如：MS_DLC.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><strong>特征</strong>条目：</p>
<p>NCF_VIRTUAL 是必需的。 NCF_HIDDEN 和 NCF_NOT_USER_REMOVABLE 是可选的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall.Services 部分</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p><em>ServiceName</em>的值<strong>AddService</strong>指令必须匹配下的筛选器组件的服务值<strong>Ndi</strong>密钥。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">Add-registry-sections</a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>创建 Ndi 密钥</p>
<p><a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Specifying service-related values](adding-service-related-values-to-the-ndi-key.md)">指定与服务相关的值</a></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">设置组件的静态参数</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">需安装另一个网络组件</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)"><strong>INF 字符串部分</strong></a></p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>没有特定于网络的要求。</p></td>
</tr>
</tbody>
</table>

 

 

 





