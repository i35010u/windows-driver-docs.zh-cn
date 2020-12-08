---
title: 使用纵横比和自定义缩放模式
description: 使用纵横比和自定义缩放模式
keywords:
- 纵横比调整 WDK 显示
- 自定义缩放 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a57a576c5599704315ece73f8083537d0a467f01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826579"
---
# <a name="using-aspect-ratio-and-custom-scaling-modes"></a>使用纵横比和自定义缩放模式


若要支持纵横比，请从 Windows 7 (（其中 **DXGKDDI \_ 接口 \_ 版本** DXGKDDI interface 版本) WIN7）开始保留扩展的缩放模式和自定义缩放模式 &gt; =  ，将以下功能添加到显示微型端口驱动程序使用的 VidPN 显示路径数据中： **\_ \_ \_**

-   [**D3DKMDT \_VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support) 结构：

    **AspectRatioCenteredMax** 和 **自定义** 成员

-   [**D3DKMDT \_VIDPN \_ 显示 \_ 路径 \_ 缩放**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling) 枚举：

    **D3DKMDT \_VPPS \_ ASPECTRATIOCENTEREDMAX** 和 **D3DKMDT \_ VPPS \_ 自定义** 值

### <a name="span-idspecifying_scaling_modesspanspan-idspecifying_scaling_modesspan-specifying-scaling-modes"></a><span id="specifying_scaling_modes"></span><span id="SPECIFYING_SCALING_MODES"></span> 指定缩放模式

[缩放桌面映像](scaling-the-desktop-image.md)中介绍了使用这些缩放模式的监视器上桌面的行为和外观。 当显示模式管理器 (CALL CENTER.DMM) 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 函数时，驱动程序必须根据 VIDPN 显示路径支持的缩放类型设置 [**D3DKMDT \_ VIDPN \_ 现有 \_ 路径 \_ 缩放 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support) 的成员，如下所示：

<span id="________Identity_Scaling_______"></span><span id="________identity_scaling_______"></span><span id="________IDENTITY_SCALING_______"></span> 标识缩放   
如果路径可以显示不带转换的内容，请将 [**D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)的 **标识** 成员设置为非零值。 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)时，请将 [**D3DKMDT \_ vidpn \_ 显示 \_ 路径 \_ 转换**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_transformation)结构的 **缩放** 成员设置为 **D3DKMDT \_ VPPS \_ 标识**。

<span id="________Centered_Scaling_______"></span><span id="________centered_scaling_______"></span><span id="________CENTERED_SCALING_______"></span> 居中缩放   
如果路径可以在目标上以无比例显示内容并居中显示，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持。居中**。 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 时，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 转换。缩放** 到 **D3DKMDT \_ VPPS \_ 居中**。

<span id="________Stretched_Scaling_______"></span><span id="________stretched_scaling_______"></span><span id="________STRETCHED_SCALING_______"></span> 延伸缩放   
如果路径可以显示缩放以适合目标的内容，而不保留源的纵横比，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持。拉伸**。 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 时，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 转换。横向扩展** 到 **D3DKMDT \_ VPPS \_**。

<span id="________Aspect-Ratio-Preserving_Stretched_Scaling_______"></span><span id="________aspect-ratio-preserving_stretched_scaling_______"></span><span id="________ASPECT-RATIO-PRESERVING_STRETCHED_SCALING_______"></span> 纵横比-保留延伸比例   
如果路径可以缩放源内容以适合目标，同时保留源的纵横比，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持。AspectRatioCenteredMax**。 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 时，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 转换。缩放** 到 **D3DKMDT \_ VPPS \_ ASPECTRATIOCENTEREDMAX**。

<span id="________Custom_Scaling_______"></span><span id="________custom_scaling_______"></span><span id="________CUSTOM_SCALING_______"></span> 自定义缩放   
如果路径可显示一个或多个未被其他 [**D3DKMDT \_ vidpn \_ 显示 \_ 路径 \_ 缩放 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support) 结构成员描述的缩放模式，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 缩放 \_ 支持。自定义**。 调用 [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 时，请设置 **D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 转换。缩放** 到 **D3DKMDT \_ VPPS \_ 自定义**。 独立硬件供应商 (Ihv) 可以使用私有转义值通知驱动程序如何解释给定目标上的自定义缩放。

如果当前固定目标和源模式具有相同的纵横比，但大小不同，则显示微型端口驱动程序应仅设置 **延伸** 和 **居中** 的成员。 在这种情况下，CALL CENTER.DMM 将清除 **AspectRatioCenteredMax** 成员的任何非零值。

### <a name="span-idapi_to_ddi_scalingspanspan-idapi_to_ddi_scalingspan-api-to-ddi-scaling"></a><span id="api_to_ddi_scaling"></span><span id="API_TO_DDI_SCALING"></span> API 到 DDI 缩放

下表显示了用户模式 API 缩放值到显示微型端口驱动程序的 [**D3DKMDT \_ VIDPN 显示 \_ \_ 路径 \_ 缩放**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling) 枚举值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="/windows/win32/api/winuser/nf-winuser-setdisplayconfig" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](/windows/win32/api/winuser/nf-winuser-setdisplayconfig)"><strong>SetDisplayConfig</strong></a> API 缩放值</th>
<th align="left">DDI 缩放值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>D3DKMDT_VPPS_IDENTITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>D3DKMDT_VPPS_CENTERED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>D3DKMDT_VPPS_STRETCHED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPRATIOMAX</p></td>
<td align="left"><p>D3DKMDT_VPPS_ASPECTRATIOCENTEREDMAX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>D3DKMDT_VPPS_CUSTOM</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>D3DKMDT_VPPS_PREFERRED</p></td>
</tr>
</tbody>
</table>

 

此映射可用于 [缩放桌面图像](scaling-the-desktop-image.md) 中的表，以了解用户模式缩放类型如何转换为发送到显示微型端口驱动程序的 DDI 缩放类型。

### <a name="span-idscaling_and_driver_versionsspanspan-idscaling_and_driver_versionsspan-scaling-and-driver-versions"></a><span id="scaling_and_driver_versions"></span><span id="SCALING_AND_DRIVER_VERSIONS"></span> 缩放和驱动程序版本

下表显示了在不同版本的操作系统上运行的不同显示微型端口驱动程序版本的行为。

驱动程序版本操作系统版本

**DXGKDDI \_接口 \_ 版本** &lt; **DXGKDDI \_ 接口 \_ 版本 \_ WIN7**

和

&gt;= **DXGKDDI \_ 接口 \_ 版本 \_ VISTA**

**DXGKDDI \_接口 \_ 版本** &gt; =  **DXGKDDI \_ 接口 \_ 版本 \_ WIN7**

Windows Vista

驱动程序具有 Windows Vista 行为。

驱动程序必须在初始化期间检查操作系统的版本，并且决不应公开或使用 **D3DKMDT \_ VIDPN \_ 提供 \_ \_ \_ 支持** 的 **AspectRatioCenteredMax** 和 **自定义** 成员。 如果驱动程序违反了此要求，则 CALL CENTER.DMM 将忽略 **AspectRatioCenteredMax** 和 **Custom** ，并仅识别 **标识**、 **居中** 或 **延伸** 成员。 如果驱动程序尝试固定任何 VidPN 路径上的 **D3DKMDT \_ VPPS \_ ASPECTRATIOCENTEREDMAX** 缩放模式，call center.dmm 将返回状态代码 **状态 \_ 图形 \_ 无效 \_ 路径 \_ 内容 \_ 几何 \_ 转换** ，并将此缩放模式视为与全屏幕拉伸模式相同。

Windows 7

操作系统将清除 **AspectRatioCenteredMax** 和 **自定义** 成员的值，并假定该驱动程序不支持纵横比-保留延伸缩放和自定义缩放模式。 CALL CENTER.DMM 只会设置缩放模式 **D3DKMDT \_ VPPS \_ IDENTITY**、 **D3DKMDT \_ VPPS \_ 伸展** 或 **D3DKMDT \_ VPPS \_ 居中**。 驱动程序在 Windows Vista 上的行为类似。

驱动程序应支持 **AspectRatioCenteredMax** 成员，并且操作系统从 "控制面板" 应用程序使用它。 驱动程序可以选择通过设置 **自定义** 成员来实现自定义功能。

 

Call center.dmm 将始终确认驱动程序接口 &gt; =  **DXGKDDI \_ 接口 \_ 版本 \_ WIN7** ，然后再尝试检查并使用 [**D3DKMDT \_ VIDPN \_ 提供 \_ \_ \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)的 **AspectRatioCenteredMax** 或 **自定义** 成员。

**重要提示**   支持 **D3DKMDT \_ VPPS \_ ASPECTRATIOCENTEREDMAX** 或 **D3DKMDT \_ VPPS \_ 自定义** 值的显示微型端口驱动程序绝不应将值设置为 **D3DKMDT \_ VPPS \_ NOTSPECIFIED**。

 

### <a name="span-idscaling_with_multiple_adaptersspanspan-idscaling_with_multiple_adaptersspan-scaling-with-multiple-adapters"></a><span id="scaling_with_multiple_adapters"></span><span id="SCALING_WITH_MULTIPLE_ADAPTERS"></span> 缩放多个适配器

随 Windows 7 引入的缩放类型 **D3DKMDT \_ VPPS \_ ASPECTRATIOCENTEREDMAX** 和 **D3DKMDT \_ VPPS \_ 自定义** 的值存储在与 (GPU) 的图形处理单元关联的 CCD 连接数据库中。 如果用户将监视器从支持这些缩放成员的驱动程序移动到另一个 GPU，则原始驱动程序可能不支持第二个 GPU。 在这种情况下，操作系统会将这些缩放类型映射到系统默认缩放。

如果两个 Gpu 都支持缩放类型 **D3DKMDT \_ VPPS \_ ASPECTRATIOCENTEREDMAX** 和 **D3DKMDT \_ VPPS \_ custom**，并且第一个 GPU 的驱动程序实现了 **D3DKMDT \_ VPPS \_ 自** 定义缩放请求，则当用户将监视器切换到第二个 gpu 时，第二个 gpu 的驱动程序可能不知道如何解释自定义的缩放请求。 在这种情况下，第二个驱动程序应失败对 [**DxgkDdiCommitVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn) 函数的调用，并且应返回 **状态 \_ 图形 \_ VIDPN \_ 模态 \_ 不 \_ 受支持** 的状态代码; 操作系统将此缩放类型映射到系统默认缩放。

