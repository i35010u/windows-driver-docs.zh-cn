---
title: WDDM 1.2 中的图形 INF 要求
description: 在 Windows 8 的 Windows 显示器驱动程序模型 (WDDM) 驱动程序需要图形驱动程序 INF 更改。
ms.assetid: BB1E35B4-8691-4B0C-9D6C-9A7D1ADFAB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37806f8c74e01be0133a54946e5616b64dfb6462
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349166"
---
# <a name="graphics-inf-requirements-in-wddm-12"></a>WDDM 1.2 中的图形 INF 要求


在 Windows 8 的 Windows 显示器驱动程序模型 (WDDM) 驱动程序需要图形驱动程序 INF 更改。 最显著的变化是在功能得分。 WDDM 1.2 驱动程序需要较高的功能得分比早期版本的 WDDM 驱动程序。 本部分介绍 Windows 8 图形驱动程序相关的所有 INF 要求

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="updated-feature-score-directive.md" data-raw-source="[Updated feature score directive in Windows 8](updated-feature-score-directive.md)">在 Windows 8 中的更新的功能分数指令</a></p></td>
<td align="left"><p>更新的功能分数指令是具有所需的所有 Windows 8 驱动程序遵循 WDDM 的常规安装设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-matching-criteria.md" data-raw-source="[Driver matching criteria](driver-matching-criteria.md)">驱动程序匹配条件</a></p></td>
<td align="left"><p>本主题描述用于选择驱动程序的最佳匹配项的元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="updated-friendly-name.md" data-raw-source="[Updated friendly name for WDDM 1.2](updated-friendly-name.md)">WDDM 1.2 的新友好名称</a></p></td>
<td align="left"><p>本主题介绍图形 INF 的新友好名称。 这是所有 Windows 8 中框显示驱动程序 Inf 可本地化的字符串名称要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="sku-differentiation-directive.md" data-raw-source="[SKU differentiation directive](sku-differentiation-directive.md)">SKU 差异化指令</a></p></td>
<td align="left"><p>使用 Windows Server 2008 和 Windows Vista SP1 中，框中显示驱动程序 Inf 已修改为包括一个新值，表示作为驱动程序<em>客户端仅</em>，驱动程序将不在服务器 Sku 的 Windows 安装的含义。 此指令时在 Windows 8 中的所有显示器驱动程序的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-unicode-requirement.md" data-raw-source="[General Unicode requirement in INF files](general-unicode-requirement.md)">INF 文件中的常规 Unicode 要求</a></p></td>
<td align="left"><p>应保存 INF 文件，并将其编码为 unicode 格式;它们不能 ANSI。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="installed-display-drivers-directive.md" data-raw-source="[Installed display drivers directive](installed-display-drivers-directive.md)">已安装的显示驱动程序指令</a></p></td>
<td align="left"><p>已安装的显示驱动程序指令是恰当的名称为驱动程序包的一部分安装 UMD 软件设备设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="copy-flags-to-support-pnp-stop-directive.md" data-raw-source="[Copy flags to support PnP stop directive](copy-flags-to-support-pnp-stop-directive.md)">复制标志来支持即插即用的 stop 指令</a></p></td>
<td align="left"><p>需要以支持不需要重新启动的驱动程序升级的 WDDM 插即用 (PnP) 停止指令的文件部分标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-services-start-type-directive.md" data-raw-source="[Driver\services start type directive](driver-services-start-type-directive.md)">Driver\services 启动 type 指令</a></p></td>
<td align="left"><p><em>Driver\services</em>开始 type 指令是服务安装设置必需的所有显示器驱动程序。 WDDM 驱动程序是插即用 (PnP)，因此必须按需启动，其中<em>StartType</em> = 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="capability-override-settings-to-disable-opengl.md" data-raw-source="[Capability override settings to disable OpenGL](capability-override-settings-to-disable-opengl.md)">功能重写的设置为禁用 OpenGL</a></p></td>
<td align="left"><p>所有的框中显示 Inf 此软件设备设置可确保没有现成的驱动程序将面临开箱 OpenGL ICDs 的互操作性问题。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-version--section-directives.md" data-raw-source="[[Version] section directives](-version--section-directives.md)">[Version] 部分指令</a></p></td>
<td align="left"><p>本主题介绍<em>[Version]</em>部分 INF 中的指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="-sourcedisknames--section-directives.md" data-raw-source="[[SourceDiskNames] section directives](-sourcedisknames--section-directives.md)">[SourceDiskNames] 部分指令</a></p></td>
<td align="left"><p>Windows Vista 及更高版本，内置使用 Inf <em>[SourceDisksXxx]</em>指令。 但是，这些部分的值已从内容具有先前通常已记下独立硬件供应商 (IHV) 生产驱动程序包中更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="general-x64-directives.md" data-raw-source="[General x64 directives](general-x64-directives.md)">常规 x 64 指令</a></p></td>
<td align="left"><p>本主题介绍正确修饰在 64 位 Windows 上使用 INF 所需的更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-install-section-directives.md" data-raw-source="[General install section directives](general-install-section-directives.md)">常规安装部分指令</a></p></td>
<td align="left"><p>这是对开箱或生产/发布的二进制文件、 服务、 regadd 或 delreg 部分通常属于零售 WHQL 驱动程序包的所有引用程序未都列在 Windows 中内置驱动程序包的常规提醒。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-string--section-changes-for-localized-strings.md" data-raw-source="[[String] section changes for localized strings](-string--section-changes-for-localized-strings.md)">用于本地化的字符串 [string] 部分更改</a></p></td>
<td align="left"><p>此 INF 要求确保伪本地化时生成的工作。 要求是描述可与字符串部分中的非可本地化的字符串本地化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md" data-raw-source="[Driver DLL for display adapter or chipset has properly formatted file version](driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md)">显示适配器或芯片组驱动程序 DLL 具有正确格式的文件版本</a></p></td>
<td align="left"><p>本主题介绍了显示器驱动程序 Dll 的正确格式设置。</p></td>
</tr>
</tbody>
</table>

 

 

 





