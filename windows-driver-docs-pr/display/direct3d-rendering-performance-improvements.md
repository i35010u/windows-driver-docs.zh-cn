---
title: Direct3D 呈现性能改进
description: Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以支持 Microsoft Direct3D 呈现性能改进，让 Direct3D 9 的硬件更好地利用硬件命令缓冲区和计数器和高效复制到系统内存子。 这些功能，镜像的一些功能可用于 Direct3D 版本 10 硬件，是从 Windows 8.1 新功能。
ms.assetid: F9AAE489-EC45-4EE6-875E-E084BB3054EE
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: cbed8871a27bf3aec88a928492c1d822f06d398c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349498"
---
# <a name="direct3d-rendering-performance-improvements"></a>Direct3D 呈现性能改进


Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以支持 Microsoft Direct3D 呈现性能改进，让 Direct3D 9 的硬件更好地利用硬件命令缓冲区和计数器和高效复制到系统内存子。 这些功能，镜像的一些功能可用于 Direct3D 版本 10 硬件，是从 Windows 8.1 新功能。

剪裁的新 Direct3D 11.1 资源和映射默认性能改进，还提供。 下面的行为更改部分中概述了映射默认方案。

## <a name="span-idrenderingperformancereferencespanspan-idrenderingperformancereferencespanspan-idrenderingperformancereferencespanrendering-performance-reference"></a><span id="Rendering_performance_reference"></span><span id="rendering_performance_reference"></span><span id="RENDERING_PERFORMANCE_REFERENCE"></span>呈现性能参考


本参考部分描述的用户模式设备驱动程序接口 (DDIs)。

### <a name="direct3d-rendering-performance-functions-implemented-by-the-user-mode-driver"></a>由用户模式驱动程序实现的 Direct3D 呈现性能函数

本部分包含函数，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序实现以支持 Microsoft Direct3D 呈现性能改进。


|||
|:--|:--|
|[PFND3DDDI_FLUSH1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)| [PFND3DDDI_CHECKCOUNTERINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)|
|[PFND3DDDI_CHECKCOUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter) |[PFND3DDDI_UPDATESUBRESOURCEUP](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)|

### <a name="direct3d-rendering-performance-structures-and-enumerations"></a>Direct3D 呈现性能结构和枚举

这些用户模式下结构和枚举支持呈现性能改进，并且新的或更新的 Windows 8.1。 所有适用于 Direct3D 9 级驱动程序除外[ **D3D11\_1\_DDI\_刷新\_标志**](https://msdn.microsoft.com/library/windows/hardware/hh451049)。

-   [**D3DDDI\_刷新\_标志**](https://msdn.microsoft.com/library/windows/hardware/dn449154) （新）
-   [**D3DDDIARG\_COPYFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/dn449151) （新）
-   [**D3DDDIARG\_计数器\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn449152) （新）
-   [**D3DDDIARG\_UPDATESUBRESOURCEUP** ](https://msdn.microsoft.com/library/windows/hardware/dn449153) （新）
-   [**D3DDDICAPS\_简单\_INSTANCING\_支持**](https://msdn.microsoft.com/library/windows/hardware/dn465882) （新）
-   [*CreateResource2* ](https://msdn.microsoft.com/library/windows/hardware/hh406287) (WDDM 1.3 和更高版本的 Direct3D 9 级驱动程序必须返回**E\_INVALIDARG**错误代码如果**CaptureBuffer**设置的标志值)
-   [**D3D11\_1\_DDI\_刷新\_标志**](https://msdn.microsoft.com/library/windows/hardware/hh451049) (**D3DWDDM1\_3DDI\_剪裁\_内存**常量添加）
-   [**D3DDDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff544519) (**pfnFlush1**， **pfnCheckCounterInfo**， **pfnCheckCounter**， **pfnUpdateSubresourceUP**添加成员)
-   [**D3DDDI\_池**](https://msdn.microsoft.com/library/windows/hardware/ff544634) (**D3DDDIPOOL\_STAGINGMEM**常量添加)
-   [**D3DDDICAPS\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff544132) (**D3DDDICAPS\_获取\_简单\_INSTANCING\_支持**常量添加)
-   [*GetCaps* ](https://msdn.microsoft.com/library/windows/hardware/ff566762) （备注中的新信息）

## <a name="span-idddiimplementationrequirementsstartingwithwddm13spanspan-idddiimplementationrequirementsstartingwithwddm13spanddi-implementation-requirements-starting-with-wddm-13"></a><span id="ddi_implementation_requirements_starting_with_wddm_1.3"></span><span id="DDI_IMPLEMENTATION_REQUIREMENTS_STARTING_WITH_WDDM_1.3"></span>从开始 WDDM 1.3 DDI 实现要求


从 WDDM 1.3 开始，以下函数是必需或可选的用户模式驱动程序来实现。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数组</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_9_functions_that_are_optional_prior_to__1.3._Now_required_"></span><span id="_9_functions_that_are_optional_prior_to__1.3._now_required_"></span><span id="_9_FUNCTIONS_THAT_ARE_OPTIONAL_PRIOR_TO__1.3._NOW_REQUIRED_"></span>是可选的 WDDM 1.3 之前的 Direct3D 9 函数。 现在要求：</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406236" data-raw-source="[&lt;em&gt;BufBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406236)"><em>BufBlt1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406287" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406287)"><em>CreateResource2</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439866" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439866)"><em>TexBlt1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439911" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439911)"><em>VolBlt1</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_9_functions_that_are_available_starting_with__1.3._A_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_functions_that_are_available_starting_with__1.3._a_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_FUNCTIONS_THAT_ARE_AVAILABLE_STARTING_WITH__1.3._A_DRIVER_MUST_EITHER_IMPLEMENT_ALL_OF_THESE_FUNCTIONS_OR_NONE_OF_THEM_"></span>使用 WDDM 1.3 开始提供的 Direct3D 9 函数。 驱动程序必须实现所有这些函数或其中任何一个：</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449227" data-raw-source="[&lt;em&gt;pfnCheckCounter&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449227)"><em>pfnCheckCounter</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449228" data-raw-source="[&lt;em&gt;pfnCheckCounterInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449228)"><em>pfnCheckCounterInfo</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449229" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449229)"><em>pfnFlush1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn458010" data-raw-source="[&lt;em&gt;pfnPresent1(D3D)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn458010)"><em>pfnPresent1(D3D)</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn469267" data-raw-source="[&lt;em&gt;pfnPresent1(DXGI)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn469267)"><em>pfnPresent1(DXGI)</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449230" data-raw-source="[&lt;em&gt;pfnUpdateSubresourceUP&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449230)"><em>pfnUpdateSubresourceUP</em></a></li>
<li>pfnSetMarker</li>
<li>pfnSetMarkerMode</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="When_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="when_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="WHEN_THE__1.3_AND_LATER_OPTIONAL_FUNCTIONS_IMMEDIATELY_ABOVE_ARE_IMPLEMENTED__THESE_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>WDDM 1.3 和更高版本的可选函数上方紧实现时，这些函数具有相关联的行为更改：</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff538252" data-raw-source="[&lt;em&gt;BltDXGI&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538252)"><em>BltDXGI</em> </a> — 本机过渡环境</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406235" data-raw-source="[&lt;em&gt;Blt1DXGI&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406235)"><em>Blt1DXGI</em> </a> — 本机过渡环境</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406287" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406287)"><em>CreateResource2</em> </a> — 本机过渡环境、 大型捕获纹理</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff566762" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566762)"><em>GetCaps</em> </a> -时间戳，简单实例化</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff568213" data-raw-source="[&lt;em&gt;Lock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568213)"><em>锁</em></a> — 本机过渡环境</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439866" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439866)"><em>TexBlt1</em> </a> — 本机过渡环境</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff570104" data-raw-source="[&lt;em&gt;Unlock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570104)"><em>解锁</em></a> — 本机过渡环境</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439911" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439911)"><em>VolBlt1</em> </a> — 本机过渡环境</li>
</ul>
<p>这些方案应用何时<a href="https://msdn.microsoft.com/library/windows/hardware/ff566762" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566762)"> <em>GetCaps</em> </a>调用：</p>
<ul>
<li>如果<strong>D3DDDICAPS_GETD3DQUERYDATA</strong> ，则该驱动程序 （可选） 可以报告对时间戳，这意味着 Direct3D 运行时不会屏蔽的支持的支持。</li>
<li>如果<strong>D3DDDICAPS_GET_SIMPLE_INSTANCING_SUPPORT</strong> ，则该驱动程序可以报告的可选硬件支持实例化。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="These__11_functions_have_associated_behavior_changes_"></span><span id="these__11_functions_have_associated_behavior_changes_"></span><span id="THESE__11_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>这些 Direct3D 11 函数具有关联的行为更改：</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"><em>CreateResource(D3D11)</em> </a> — 缓冲区映射默认值 （请参阅以下部分的行为更改）</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449229" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449229)"><em>pfnFlush1</em></a> — resource trim</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff569492" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569492)"><em>ResourceMap</em> </a> — 缓冲区映射默认值 （请参阅以下部分的行为更改）</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff569495" data-raw-source="[&lt;em&gt;ResourceUnmap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569495)"><em>ResourceUnmap</em> </a> — 缓冲区映射默认值 （请参阅以下部分的行为更改）</li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idbehaviorspanspan-idbehaviorspanbehavior-changes-for-calls-to-resource-create-map-and-unmap-functions"></a><span id="_behavior_"></span><span id="_BEHAVIOR_"></span>创建、 映射和取消映射函数的调用资源的行为更改


对于由 WDDM 1.3 和更高版本的驱动程序实现这些函数，Direct3D 运行时会提供一组受限的默认方案，映射的输入值。 这些受限制的值仅适用于支持功能级别 11.1 及更高版本的驱动程序。

[***CreateResource(D3D11)***](https://msdn.microsoft.com/library/windows/hardware/ff540694) **function**—

这些输入[ **D3D11DDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542062)结构成员是受限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ResourceDimension_and_Usage"></span><span id="resourcedimension_and_usage"></span><span id="RESOURCEDIMENSION_AND_USAGE"></span><strong>ResourceDimension</strong>和<strong>使用情况</strong></p></td>
<td align="left"><p>这些行为更改仅适用于 Direct3D 运行时会提供类型<strong>D3D10DDIRESOURCE_BUFFER</strong>有关<strong>ResourceDimension</strong>并键入<strong>D3D10_DDI_USAGE_DEFAULT</strong>有关<strong>使用情况</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="BindFlags"></span><span id="bindflags"></span><span id="BINDFLAGS"></span><strong>BindFlags</strong></p></td>
<td align="left"><p>Direct3D 运行时设置只<strong>D3D10_DDI_BIND_SHADER_RESOURCE</strong>并<strong>D3D11_DDI_BIND_UNORDERED_ACCESS</strong>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MapFlags"></span><span id="mapflags"></span><span id="MAPFLAGS"></span><strong>MapFlags</strong></p></td>
<td align="left"><p>如果满足所有其他成员此处列出的要求，可以设置运行时<strong>D3D10_DDI_MAP_READ</strong>， <strong>D3D10_DDI_MAP_WRITE</strong>，并<strong>D3D10_DDI_MAP_READWRITE</strong>值。 该驱动程序必须支持这些值。 值<strong>D3D10_DDI_MAP_WRITE_DISCARD</strong>并<strong>D3D10_DDI_MAP_WRITE_NOOVERWRITE</strong>无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MiscFlags"></span><span id="miscflags"></span><span id="MISCFLAGS"></span><strong>MiscFlags</strong></p></td>
<td align="left"><p>在运行时设置只<strong>D3D11_DDI_RESOURCE_MISC_BUFFER_ALLOW_RAW_VIEWS</strong>并<strong>D3D11_DDI_RESOURCE_MISC_BUFFER_STRUCTURED</strong>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Format"></span><span id="format"></span><span id="FORMAT"></span><strong>格式</strong></p></td>
<td align="left"><p>在运行时设置只<strong>DXGI_FORMAT_UNKNOWN</strong>值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="SampleDesc"></span><span id="sampledesc"></span><span id="SAMPLEDESC"></span><strong>SampleDesc</strong></p></td>
<td align="left"><p>运行时设置<a href="https://msdn.microsoft.com/library/windows/desktop/bb173072" data-raw-source="[&lt;strong&gt;DXGI_SAMPLE_DESC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/bb173072)"> <strong>DXGI_SAMPLE_DESC</strong></a>。<strong>计数</strong>为 1，成员和<strong>质量</strong>为零的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MipLevels"></span><span id="miplevels"></span><span id="MIPLEVELS"></span><strong>MipLevels</strong></p></td>
<td align="left"><p>在运行时将值设置为 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ArraySize"></span><span id="arraysize"></span><span id="ARRAYSIZE"></span><strong>ArraySize</strong></p></td>
<td align="left"><p>在运行时将值设置为 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="pPrimaryDesc"></span><span id="pprimarydesc"></span><span id="PPRIMARYDESC"></span><strong>pPrimaryDesc</strong></p></td>
<td align="left"><p>在运行时将值设置为<strong>NULL</strong>。</p></td>
</tr>
</tbody>
</table>

 

[***ResourceMap***](https://msdn.microsoft.com/library/windows/hardware/ff569492) **function**—

这些输入参数[ *ResourceMap* ](https://msdn.microsoft.com/library/windows/hardware/ff569492)限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>Direct3D 运行时设置只<strong>D3D10DDIRESOURCE_BUFFER</strong>资源时为非零值<em>MapFlags</em>创建调用中设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><span></span><em></em></p></td>
<td align="left"><p>在运行时设置只<strong>DXGI_FORMAT_UNKNOWN</strong>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>子资源</em></p></td>
<td align="left"><p>在运行时仅将值设置为 0。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DDIMap"></span><span id="ddimap"></span><span id="DDIMAP"></span><em>DDIMap</em></p></td>
<td align="left"><p>如果满足所有其他成员此处列出的要求，可以设置运行时<strong>D3D10_DDI_MAP_READ</strong>， <strong>D3D10_DDI_MAP_WRITE</strong>，或<strong>D3D10_DDI_MAP_READWRITE</strong>值，匹配<em>MapFlags</em>值设置在创建调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span><em>标志</em></p></td>
<td align="left"><p>尽管从运行时输入的值不是受限制，但该驱动程序必须能够支持<strong>D3D10_DDI_MAP_FLAG_DONOTWAIT</strong>值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="pMappedSubResource"></span><span id="pmappedsubresource"></span><span id="PMAPPEDSUBRESOURCE"></span>pMappedSubResource</p></td>
<td align="left"><p>尽管从运行时输入的值不是受限制，但驱动程序必须将分配到的有效 CPU 可缓存指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff541839" data-raw-source="[&lt;strong&gt;D3D10DDI_MAPPED_SUBRESOURCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541839)"> <strong>D3D10DDI_MAPPED_SUBRESOURCE</strong></a>。<strong>pData</strong>成员，必须设置<strong>RowPitch</strong>并<strong>DepthPitch</strong>以匹配缓冲区和中提供的数据的大小<strong>pData</strong>。</p></td>
</tr>
</tbody>
</table>

 

[***ResourceUnmap***](https://msdn.microsoft.com/library/windows/hardware/ff569495) **function**—

这些输入参数[ *ResourceUnmap* ](https://msdn.microsoft.com/library/windows/hardware/ff569495)限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hDevice"></span><span id="hdevice"></span><span id="HDEVICE"></span><em>hDevice</em></p></td>
<td align="left"><p>尽管从 Direct3D 运行时输入的值不是受限制，但与匹配的值<em>hDevice</em>值与原始<a href="https://msdn.microsoft.com/library/windows/hardware/ff569492" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569492)"> <em>ResourceMap</em> </a>调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>在运行时设置只<strong>D3D10DDIRESOURCE_BUFFER</strong>资源时为非零值<em>MapFlags</em>创建调用中设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>子资源</em></p></td>
<td align="left"><p>在运行时仅将值设置为 0。</p></td>
</tr>
</tbody>
</table>

 

 

 





