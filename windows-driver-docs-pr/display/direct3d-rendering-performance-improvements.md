---
title: Direct3D 呈现性能改进
description: Windows 显示器驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序可以支持 Microsoft Direct3D 渲染性能改进，使 Direct3D 9 硬件可以更好地使用硬件命令缓冲区和计数器，并将系统内存的有效副本子资源。 这些功能镜像了 Direct3D 版本10硬件可用的一些功能，是从 Windows 8.1 开始的新功能。
ms.assetid: F9AAE489-EC45-4EE6-875E-E084BB3054EE
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 10da5d658ffa78d291594d1634a443801a796200
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107308"
---
# <a name="direct3d-rendering-performance-improvements"></a>Direct3D 呈现性能改进


Windows 显示器驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序可以支持 Microsoft Direct3D 渲染性能改进，使 Direct3D 9 硬件可以更好地使用硬件命令缓冲区和计数器，并将系统内存的有效副本子资源。 这些功能镜像了 Direct3D 版本10硬件可用的一些功能，是从 Windows 8.1 开始的新功能。

还提供了新的 Direct3D 11.1 资源剪裁和地图默认性能改进。 下面的行为更改部分中概述了地图的默认情况。

## <a name="span-idrendering_performance_referencespanspan-idrendering_performance_referencespanspan-idrendering_performance_referencespanrendering-performance-reference"></a><span id="Rendering_performance_reference"></span><span id="rendering_performance_reference"></span><span id="RENDERING_PERFORMANCE_REFERENCE"></span>呈现性能引用


本参考部分介绍 (DDIs) 的用户模式设备驱动程序接口。

### <a name="direct3d-rendering-performance-functions-implemented-by-the-user-mode-driver"></a>Direct3D 呈现由用户模式驱动程序实现的性能函数

本部分包含一些函数，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序实现，以支持 Microsoft Direct3D 呈现性能改进。


**[PFND3DDDI_FLUSH1](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)**： [PFND3DDDI_CHECKCOUNTERINFO](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)

**[PFND3DDDI_CHECKCOUNTER](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter)**： [PFND3DDDI_UPDATESUBRESOURCEUP](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)


### <a name="direct3d-rendering-performance-structures-and-enumerations"></a>Direct3D 呈现性能结构和枚举

这些用户模式结构和枚举支持呈现性能改进，并为 Windows 8.1 提供了新的或更新的。 All 适用于除 [**D3D11 \_ 1 \_ DDI \_ 刷新 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_flush_flags)以外的 Direct3D Level 9 驱动程序。

-   [**D3DDDI \_刷新 \_ 标记**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_flush_flags) (新的) 
-   [**D3DDDIARG \_COPYFLAGS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_copyflags) (new) 
-   [**D3DDDIARG \_计数器 \_ 信息**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_counter_info) (新的) 
-   [**D3DDDIARG \_UPDATESUBRESOURCEUP**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_updatesubresourceup) (new) 
-   [**D3DDDICAPS \_简单的 \_ 实例化 \_ 支持**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_simple_instancing_support) (新的) 
-   如果) 将**CaptureBuffer**标志值设置为，则[*CreateResource2*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2) (WDDM 1.3 及更高版本的 Direct3D Level 9 驱动程序必须返回**E \_ INVALIDARG**错误代码。
-   [**D3D11 \_ 1 \_ DDI \_ FLUSH \_ 标记**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_flush_flags) (**D3DWDDM1 \_ 3DDI \_ 剪裁 \_ 内存** 常量添加) 
-   [**D3DDDI \_**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)添加了 DEVICEFUNCS (**pfnFlush1**、 **pfnCheckCounterInfo**、 **pfnCheckCounter**、 **pfnUpdateSubresourceUP**成员) 
-   [**D3DDDI \_**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddi_pool)添加的池 (**D3DDDIPOOL \_ STAGINGMEM**常量) 
-   [**D3DDDICAPS \_输入**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type) (**D3DDDICAPS \_ 获取 \_ 简单的 \_ 实例 \_ 支持** 常数) 
-   备注中的[*GetCaps*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) (新信息) 

## <a name="span-idddi_implementation_requirements_starting_with_wddm_13spanspan-idddi_implementation_requirements_starting_with_wddm_13spanddi-implementation-requirements-starting-with-wddm-13"></a><span id="ddi_implementation_requirements_starting_with_wddm_1.3"></span><span id="DDI_IMPLEMENTATION_REQUIREMENTS_STARTING_WITH_WDDM_1.3"></span>从 WDDM 1.3 开始的 DDI 实现要求


从 WDDM 1.3 开始，对于要实现的用户模式驱动程序，以下函数是必需的或可选的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数组</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_9_functions_that_are_optional_prior_to__1.3._Now_required_"></span><span id="_9_functions_that_are_optional_prior_to__1.3._now_required_"></span><span id="_9_FUNCTIONS_THAT_ARE_OPTIONAL_PRIOR_TO__1.3._NOW_REQUIRED_"></span>在 WDDM 1.3 之前是可选的 Direct3D 9 函数。 现在需要：</p></td>
<td align="left"><ul>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_bufblt1" data-raw-source="[&lt;em&gt;BufBlt1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_bufblt1)"><em>BufBlt1</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)"><em>CreateResource2</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1)"><em>TexBlt1</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1)"><em>VolBlt1</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_9_functions_that_are_available_starting_with__1.3._A_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_functions_that_are_available_starting_with__1.3._a_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_FUNCTIONS_THAT_ARE_AVAILABLE_STARTING_WITH__1.3._A_DRIVER_MUST_EITHER_IMPLEMENT_ALL_OF_THESE_FUNCTIONS_OR_NONE_OF_THEM_"></span>从 WDDM 1.3 开始可用的 Direct3D 9 函数。 驱动程序必须实现所有这些功能，或者不使用任何一个：</p></td>
<td align="left"><ul>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter" data-raw-source="[&lt;em&gt;pfnCheckCounter&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter)"><em>pfnCheckCounter</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo" data-raw-source="[&lt;em&gt;pfnCheckCounterInfo&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)"><em>pfnCheckCounterInfo</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)"><em>pfnFlush1</em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1" data-raw-source="[&lt;em&gt;pfnPresent1(D3D)&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1)"><em>pfnPresent1 (D3D) </em></a></li>
<li><a href="/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions" data-raw-source="[&lt;em&gt;pfnPresent1(DXGI)&lt;/em&gt;](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)"><em>pfnPresent1 (DXGI) </em></a></li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup" data-raw-source="[&lt;em&gt;pfnUpdateSubresourceUP&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)"><em>pfnUpdateSubresourceUP</em></a></li>
<li>pfnSetMarker</li>
<li>pfnSetMarkerMode</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="When_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="when_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="WHEN_THE__1.3_AND_LATER_OPTIONAL_FUNCTIONS_IMMEDIATELY_ABOVE_ARE_IMPLEMENTED__THESE_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>如果实现了上述的 WDDM 1.3 和更高版本可选函数，则这些函数将具有关联的行为更改：</p></td>
<td align="left"><ul>
<li><a href="/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions" data-raw-source="[&lt;em&gt;BltDXGI&lt;/em&gt;](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)"><em>BltDXGI</em></a> —本机过渡</li>
<li><a href="/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions" data-raw-source="[&lt;em&gt;Blt1DXGI&lt;/em&gt;](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)"><em>Blt1DXGI</em></a> —本机过渡</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)"><em>CreateResource2</em></a> —本机过渡、大型捕获纹理</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)"><em>GetCaps</em></a> —时间戳，简单实例化</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock" data-raw-source="[&lt;em&gt;Lock&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)"><em>锁定</em></a> —本机过渡</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1)"><em>TexBlt1</em></a> —本机过渡</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock" data-raw-source="[&lt;em&gt;Unlock&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)"><em>解锁</em></a> —本机过渡</li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1)"><em>VolBlt1</em></a> —本机过渡</li>
</ul>
<p>调用 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)"><em>GetCaps</em></a> 时，将应用这些方案：</p>
<ul>
<li>如果设置 <strong>D3DDDICAPS_GETD3DQUERYDATA</strong> ，则驱动程序可以选择报告对时间戳的支持，这意味着 Direct3D 运行时不支持。</li>
<li>如果设置 <strong>D3DDDICAPS_GET_SIMPLE_INSTANCING_SUPPORT</strong> ，则驱动程序可以报告对实例化的可选硬件支持。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="These__11_functions_have_associated_behavior_changes_"></span><span id="these__11_functions_have_associated_behavior_changes_"></span><span id="THESE__11_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>这些 Direct3D 11 函数具有关联的行为更改：</p></td>
<td align="left"><ul>
<li><a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>CreateResource (D3D11) </em></a> —缓冲区映射默认值 (请参阅下面的行为更改部分) </li>
<li><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)"><em>pfnFlush1</em></a> -资源剪裁</li>
<li><a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><em>Windows.applicationmodel.resources.core.resourcemap</em></a> —缓冲区映射默认 (请参阅下面的行为更改部分) </li>
<li><a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap" data-raw-source="[&lt;em&gt;ResourceUnmap&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)"><em>ResourceUnmap</em></a> —缓冲区映射默认 (请参阅下面的行为更改部分) </li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-id_behavior_spanspan-id_behavior_spanbehavior-changes-for-calls-to-resource-create-map-and-unmap-functions"></a><span id="_behavior_"></span><span id="_BEHAVIOR_"></span>资源创建、映射和取消映射函数调用的行为更改


对于由 WDDM 1.3 和更高版本的驱动程序实现的这些函数，Direct3D 运行时为映射的默认方案提供一组有限的输入值。 这些限制值仅适用于支持功能级别11.1 和更高版本的驱动程序。

[***CreateResource (D3D11) ***](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource) **函数**-

以下输入 [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource) 结构成员受到限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ResourceDimension_and_Usage"></span><span id="resourcedimension_and_usage"></span><span id="RESOURCEDIMENSION_AND_USAGE"></span><strong>ResourceDimension</strong> 和 <strong>用法</strong></p></td>
<td align="left"><p>仅当 Direct3D 运行时为<strong>ResourceDimension</strong>提供类型<strong>D3D10DDIRESOURCE_BUFFER</strong> ，并键入<strong>D3D10_DDI_USAGE_DEFAULT</strong>以供<strong>使用</strong>时，这些行为更改才适用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="BindFlags"></span><span id="bindflags"></span><span id="BINDFLAGS"></span><strong>BindFlags</strong></p></td>
<td align="left"><p>Direct3D 运行时仅设置 <strong>D3D10_DDI_BIND_SHADER_RESOURCE</strong> 值和 <strong>D3D11_DDI_BIND_UNORDERED_ACCESS</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MapFlags"></span><span id="mapflags"></span><span id="MAPFLAGS"></span><strong>MapFlags</strong></p></td>
<td align="left"><p>如果满足此处列出的所有其他成员要求，则运行时可以设置 <strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>和 <strong>D3D10_DDI_MAP_READWRITE</strong> 值。 驱动程序必须支持这些值。 <strong>D3D10_DDI_MAP_WRITE_DISCARD</strong>和<strong>D3D10_DDI_MAP_WRITE_NOOVERWRITE</strong>的值无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MiscFlags"></span><span id="miscflags"></span><span id="MISCFLAGS"></span><strong>MiscFlags</strong></p></td>
<td align="left"><p>运行时仅设置 <strong>D3D11_DDI_RESOURCE_MISC_BUFFER_ALLOW_RAW_VIEWS</strong> 值和 <strong>D3D11_DDI_RESOURCE_MISC_BUFFER_STRUCTURED</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Format"></span><span id="format"></span><span id="FORMAT"></span><strong>形式</strong></p></td>
<td align="left"><p>运行时仅设置 <strong>DXGI_FORMAT_UNKNOWN</strong> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="SampleDesc"></span><span id="sampledesc"></span><span id="SAMPLEDESC"></span><strong>SampleDesc</strong></p></td>
<td align="left"><p>运行时设置<a href="/windows/desktop/api/dxgicommon/ns-dxgicommon-dxgi_sample_desc" data-raw-source="[&lt;strong&gt;DXGI_SAMPLE_DESC&lt;/strong&gt;](/windows/desktop/api/dxgicommon/ns-dxgicommon-dxgi_sample_desc)"><strong>DXGI_SAMPLE_DESC</strong></a>。将成员计数为1，将<strong>质量</strong>成员<strong>计数</strong>为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MipLevels"></span><span id="miplevels"></span><span id="MIPLEVELS"></span><strong>MipLevels</strong></p></td>
<td align="left"><p>运行时将值设置为1。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ArraySize"></span><span id="arraysize"></span><span id="ARRAYSIZE"></span><strong>数组大小</strong></p></td>
<td align="left"><p>运行时将值设置为1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="pPrimaryDesc"></span><span id="pprimarydesc"></span><span id="PPRIMARYDESC"></span><strong>pPrimaryDesc</strong></p></td>
<td align="left"><p>运行时将值设置为 <strong>NULL</strong>。</p></td>
</tr>
</tbody>
</table>

 

[***Windows.applicationmodel.resources.core.resourcemap***](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap) **函数**-

[*Windows.applicationmodel.resources.core.resourcemap*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)的这些输入参数受到限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>当在<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>CreateResource (D3D11) </em></a>的创建调用中设置<em>MapFlags</em>的非零值时，Direct3D 运行时仅设置<strong>D3D10DDIRESOURCE_BUFFER</strong>资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span></span><em></em></p></td>
<td align="left"><p>运行时仅设置 <strong>DXGI_FORMAT_UNKNOWN</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>运行时仅将值设置为0。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DDIMap"></span><span id="ddimap"></span><span id="DDIMAP"></span><em>DDIMap</em></p></td>
<td align="left"><p>如果满足此处列出的所有其他成员要求，则运行时可以设置<strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>或<strong>D3D10_DDI_MAP_READWRITE</strong>值，这些值与<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>CreateResource (D3D11) </em></a>的创建调用中设置的<em>MapFlags</em>值匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span><em>随意</em></p></td>
<td align="left"><p>尽管运行时中的输入值不受限制，但驱动程序必须能够支持 <strong>D3D10_DDI_MAP_FLAG_DONOTWAIT</strong> 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="pMappedSubResource"></span><span id="pmappedsubresource"></span><span id="PMAPPEDSUBRESOURCE"></span>pMappedSubResource</p></td>
<td align="left"><p>尽管运行时中的输入值不受限制，但驱动程序必须将有效的可通过 CPU 缓存的指针分配到 <a href="/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_mapped_subresource" data-raw-source="[&lt;strong&gt;D3D10DDI_MAPPED_SUBRESOURCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_mapped_subresource)"><strong>D3D10DDI_MAPPED_SUBRESOURCE</strong></a>。<strong>pData</strong> 成员，并且必须设置 <strong>RowPitch</strong> 和 <strong>DepthPitch</strong> ，以匹配缓冲区大小和 <strong>pData</strong>中提供的数据。</p></td>
</tr>
</tbody>
</table>

 

[***ResourceUnmap***](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap) **函数**-

[*ResourceUnmap*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)的这些输入参数受到限制：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hDevice"></span><span id="hdevice"></span><span id="HDEVICE"></span><em>hDevice</em></p></td>
<td align="left"><p>尽管 Direct3D 运行时中的输入值不受限制，但与原始<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><em>windows.applicationmodel.resources.core.resourcemap</em></a>调用中的<em>hDevice</em>值匹配的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>当在<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>CreateResource (D3D11) </em></a>的创建调用中设置<em>MapFlags</em>的非零值时，运行时将仅设置<strong>D3D10DDIRESOURCE_BUFFER</strong>资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>运行时仅将值设置为0。</p></td>
</tr>
</tbody>
</table>

 

