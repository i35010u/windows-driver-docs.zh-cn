---
title: WDDM 1.2 中的图形 INF 要求
description: Windows 8 中 (WDDM) 驱动程序的 windows 显示驱动程序模型需要对图形驱动程序进行 INF 更改。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dc845005d690533bab906ee5af3529ef345c486
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827305"
---
# <a name="graphics-inf-requirements-in-wddm-12"></a>WDDM 1.2 中的图形 INF 要求


Windows 8 中 (WDDM) 驱动程序的 windows 显示驱动程序模型需要对图形驱动程序进行 INF 更改。 最值得注意的更改是功能分数。 WDDM 1.2 驱动程序需要比早期 WDDM 驱动程序更高的功能分数。 本部分介绍 Windows 8 图形驱动程序的所有相关 INF 要求

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="updated-feature-score-directive.md" data-raw-source="[Updated feature score directive in Windows 8](updated-feature-score-directive.md)">Windows 8 中已更新的功能评分指令</a></p></td>
<td align="left"><p>更新的功能分数指令是一个常规安装设置，该设置是在 WDDM 之后的所有 Windows 8 驱动程序所必需的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-matching-criteria.md" data-raw-source="[Driver matching criteria](driver-matching-criteria.md)">驱动程序匹配条件</a></p></td>
<td align="left"><p>本主题介绍用于选择驱动程序的最佳匹配项的元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="updated-friendly-name.md" data-raw-source="[Updated friendly name for WDDM 1.2](updated-friendly-name.md)">WDDM 1.2 的已更新友好名称</a></p></td>
<td align="left"><p>本主题介绍图形 INF 的已更新的友好名称。 对于所有 Windows 8 内置的显示驱动程序 Inf，这是一个可本地化的字符串名称要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="sku-differentiation-directive.md" data-raw-source="[SKU differentiation directive](sku-differentiation-directive.md)">SKU 差分指令</a></p></td>
<td align="left"><p>对于 Windows Server 2008 和 Windows Vista SP1，已修改内置的显示驱动程序 Inf，使其包含仅将驱动程序表示为 <em>客户端</em>的新值，也就是说，驱动程序将不会安装在 Windows 的服务器 sku 上。 Windows 8 中的所有显示器驱动程序都需要此指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-unicode-requirement.md" data-raw-source="[General Unicode requirement in INF files](general-unicode-requirement.md)">INF 文件中的常规 Unicode 要求</a></p></td>
<td align="left"><p>INF 文件应保存并编码为 Unicode;它们不得为 ANSI。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="installed-display-drivers-directive.md" data-raw-source="[Installed display drivers directive](installed-display-drivers-directive.md)">已安装显示驱动程序的指令</a></p></td>
<td align="left"><p>已安装的显示驱动程序指令是一个软件设备设置，它为作为驱动程序包的一部分安装的 UMD 提供了正确的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="copy-flags-to-support-pnp-stop-directive.md" data-raw-source="[Copy flags to support PnP stop directive](copy-flags-to-support-pnp-stop-directive.md)">复制标志以支持 PnP 停止指令</a></p></td>
<td align="left"><p>WDDM 需要即插即用 (PnP) 停止指令文件部分标志，以支持不需要重新启动的驱动程序升级。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-services-start-type-directive.md" data-raw-source="[Driver\services start type directive](driver-services-start-type-directive.md)">驱动程序\服务启动类型指令</a></p></td>
<td align="left"><p><em>Driver\services</em> start type 指令是所有显示器驱动程序的服务安装设置要求。 WDDM 驱动程序即插即用 (PnP) ，因此必须先开始，其中 <em>StartType</em> = 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="capability-override-settings-to-disable-opengl.md" data-raw-source="[Capability override settings to disable OpenGL](capability-override-settings-to-disable-opengl.md)">用于禁用 OpenGL 的功能覆盖设置</a></p></td>
<td align="left"><p>对于所有内置的显示 Inf，此软件设备设置可确保无机箱内驱动程序会暴露给内置 OpenGL ICDs 可能的互操作性问题。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-version--section-directives.md" data-raw-source="[[Version] section directives](-version--section-directives.md)">[版本] 部分指令</a></p></td>
<td align="left"><p>本主题介绍 INF 中的 <em>[Version]</em> 节指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="-sourcedisknames--section-directives.md" data-raw-source="[[SourceDiskNames] section directives](-sourcedisknames--section-directives.md)">[SourceDiskNames] 节指令</a></p></td>
<td align="left"><p>在 Windows Vista 和更高版本中，使用 <em>[SourceDisksXxx]</em> 指令。 不过，这些部分的值已从先前通常在独立硬件供应商 (IHV) 生产驱动程序包中记录的内容进行了更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="general-x64-directives.md" data-raw-source="[General x64 directives](general-x64-directives.md)">常规 x64 指令</a></p></td>
<td align="left"><p>本主题介绍适当修饰用于64位 Windows 的 INF 所需的更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-install-section-directives.md" data-raw-source="[General install section directives](general-install-section-directives.md)">常规 install 节指令</a></p></td>
<td align="left"><p>这是一项一般提醒，即 Windows 内置驱动程序包中未列出对现成或生产/零售二进制文件、服务、regadd 或 delreg 部分的所有引用，这些部分通常属于零售 WHQL 驱动程序包。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-string--section-changes-for-localized-strings.md" data-raw-source="[[String] section changes for localized strings](-string--section-changes-for-localized-strings.md)">已本地化字符串的 [String] 部分更改</a></p></td>
<td align="left"><p>这项 INF 要求确保伪本地化的生成正常运行。 要求是将可本地化的字符串与字符串部分中的不可本地化的字符串进行界定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md" data-raw-source="[Driver DLL for display adapter or chipset has properly formatted file version](driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md)">显示适配器或芯片集的驱动程序 DLL 格式正确的文件版本</a></p></td>
<td align="left"><p>本主题介绍了显示驱动程序 Dll 的正确格式。</p></td>
</tr>
</tbody>
</table>

 

 

 





