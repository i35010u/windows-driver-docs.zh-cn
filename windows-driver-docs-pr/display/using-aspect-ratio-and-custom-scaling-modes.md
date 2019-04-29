---
title: 使用纵横比和自定义缩放模式
description: 使用纵横比和自定义缩放模式
ms.assetid: cafb6597-64a2-4d0f-bf7b-ab37f9a53bdc
keywords:
- 缩放 WDK 显示纵横比
- 自定义缩放的 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb3cbc649a3df2b2bdab04b14f6072914344d439
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361219"
---
# <a name="using-aspect-ratio-and-custom-scaling-modes"></a>使用纵横比和自定义缩放模式


若要支持长宽比保留外延式扩展和自定义缩放模式开始提供 Windows 7 (其中**DXGKDDI\_界面\_版本** &gt; =  **DXGKDDI\_接口\_版本\_WIN7**)，以下功能添加到 VidPN 存在路径使用的数据显示微型端口驱动程序：

-   [**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)结构：

    **AspectRatioCenteredMax**并**自定义**成员

-   [**D3DKMDT\_VIDPN\_存在\_路径\_缩放**](https://msdn.microsoft.com/library/windows/hardware/ff546706)枚举：

    **D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**并**D3DKMDT\_VPPS\_自定义**值

### <a name="span-idspecifyingscalingmodesspanspan-idspecifyingscalingmodesspan-specifying-scaling-modes"></a><span id="specifying_scaling_modes"></span><span id="SPECIFYING_SCALING_MODES"></span> 指定缩放模式

中所述的行为和使用这些缩放模式的监视器上的桌面的外观[缩放桌面映像](scaling-the-desktop-image.md)。 当显示模式下管理器 (DMM) 调用[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)函数，该驱动程序必须设置的成员[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)根据缩放，VidPN 显示路径支持，按如下所示的类型：

<span id="________Identity_Scaling_______"></span><span id="________identity_scaling_______"></span><span id="________IDENTITY_SCALING_______"></span> 标识缩放   
如果该路径可以显示与任何转换的内容，请设置**标识**的成员[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)为非零值。 当[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)调用时，设置**缩放**隶属[ **D3DKMDT\_VIDPN\_存在\_路径\_转换**](https://msdn.microsoft.com/library/windows/hardware/ff546719)结构**D3DKMDT\_VPPS\_标识**。

<span id="________Centered_Scaling_______"></span><span id="________centered_scaling_______"></span><span id="________CENTERED_SCALING_______"></span> 居中缩放   
如果可以显示路径内容缩放，以在目标上为中心，设置**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持。居中**。 当[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)调用时，设置**D3DKMDT\_VIDPN\_存在\_路径\_转换。缩放**到**D3DKMDT\_VPPS\_居中**。

<span id="________Stretched_Scaling_______"></span><span id="________stretched_scaling_______"></span><span id="________STRETCHED_SCALING_______"></span> 拉伸缩放   
如果该路径可以显示内容，将调整为适合目标，同时不保存的源的纵横比，设置**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持。拉伸**。 当[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)调用时，设置**D3DKMDT\_VIDPN\_存在\_路径\_转换。缩放**到**D3DKMDT\_VPPS\_STRETCHED**。

<span id="________Aspect-Ratio-Preserving_Stretched_Scaling_______"></span><span id="________aspect-ratio-preserving_stretched_scaling_______"></span><span id="________ASPECT-RATIO-PRESERVING_STRETCHED_SCALING_______"></span> 纵横比保留外延式缩放   
如果该路径可以缩放以适合目标，同时保持源的纵横比，设置的源内容**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持。AspectRatioCenteredMax**。 当[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)调用时，设置**D3DKMDT\_VIDPN\_存在\_路径\_转换。缩放**到**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**。

<span id="________Custom_Scaling_______"></span><span id="________custom_scaling_______"></span><span id="________CUSTOM_SCALING_______"></span> 自定义缩放   
如果该路径可以显示一个或多个未由其他描述的缩放模式[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)结构成员，设置**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持。自定义**。 当[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)调用时，设置**D3DKMDT\_VIDPN\_存在\_路径\_转换。缩放**到**D3DKMDT\_VPPS\_自定义**。 独立硬件供应商 (Ihv) 可以使用专用的转义值通知如何解释给定的目标的自定义缩放的驱动程序。

如果当前的固定的目标和源模式具有相同纵横比，但具有不同大小，应仅设置显示微型端口驱动程序**Stretched**并**居中**成员。 在这种情况下 DMM 将清除的任何非零值**AspectRatioCenteredMax**成员。

### <a name="span-idapitoddiscalingspanspan-idapitoddiscalingspan-api-to-ddi-scaling"></a><span id="api_to_ddi_scaling"></span><span id="API_TO_DDI_SCALING"></span> DDI 缩放 API

缩放值显示微型端口驱动程序 DDI 缩放到的用户模式 API 的对应关系中的值[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放**](https://msdn.microsoft.com/library/windows/hardware/ff546706)枚举下表中所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff569533" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569533)"><strong>SetDisplayConfig</strong> </a>缩放值的 API</th>
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

 

此映射可用于在表[缩放桌面映像](scaling-the-desktop-image.md)若要了解如何将用户模式缩放类型转换为 DDI 缩放发送到显示微型端口驱动程序的类型。

### <a name="span-idscalinganddriverversionsspanspan-idscalinganddriverversionsspan-scaling-and-driver-versions"></a><span id="scaling_and_driver_versions"></span><span id="SCALING_AND_DRIVER_VERSIONS"></span> 缩放和驱动程序版本

下表中显示不同版本的操作系统上运行不同的显示微型端口驱动程序版本的行为。

驱动程序版本的操作系统版本

**DXGKDDI\_INTERFACE\_VERSION** &lt; **DXGKDDI\_INTERFACE\_VERSION\_WIN7**

和

&gt;= **DXGKDDI\_INTERFACE\_VERSION\_VISTA**

**DXGKDDI\_INTERFACE\_VERSION** &gt;= **DXGKDDI\_INTERFACE\_VERSION\_WIN7**

Windows Vista

该驱动程序有 Windows Vista 的行为。

该驱动程序必须在初始化期间检查操作系统版本和应永远不会公开或使用**AspectRatioCenteredMax**并**自定义**的成员**D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**。 如果该驱动程序不符合此要求，将忽略 DMM **AspectRatioCenteredMax**并**自定义**并将仅识别**标识**，**居中**，或**Stretched**成员。 如果驱动程序将尝试将固定**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**任何 VidPN 路径上缩放模式下，DMM 将返回状态代码**状态\_图形\_无效\_路径\_内容\_GEOMETRY\_转换**并会将此缩放模式相同视为全屏幕拉伸模式。

Windows 7

操作系统清除的值**AspectRatioCenteredMax**并**自定义**成员，并假定该驱动程序不支持长宽比保留外延式扩展和自定义扩展模式。 仅缩放模式设置 DMM **D3DKMDT\_VPPS\_标识**， **D3DKMDT\_VPPS\_STRETCHED**，或**D3DKMDT\_VPPS\_居中**。 Windows Vista 上的驱动程序行为。

该驱动程序应支持**AspectRatioCenteredMax**成员和操作系统使用它从控制面板应用程序。 该驱动程序可以选择实现的自定义的功能，通过设置**自定义**成员。

 

DMM 将始终确认驱动程序接口&gt; =  **DXGKDDI\_接口\_版本\_WIN7**会尝试检查并使用之前**AspectRatioCenteredMax**或**自定义**的成员[ **D3DKMDT\_VIDPN\_存在\_路径\_缩放\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546712)。

**重要**  显示微型端口驱动程序支持**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**或者**D3DKMDT\_VPPS\_自定义**值应永远不会设置的值**D3DKMDT\_VPPS\_NOTSPECIFIED**。

 

### <a name="span-idscalingwithmultipleadaptersspanspan-idscalingwithmultipleadaptersspan-scaling-with-multiple-adapters"></a><span id="scaling_with_multiple_adapters"></span><span id="SCALING_WITH_MULTIPLE_ADAPTERS"></span> 使用多个适配器进行缩放

缩放类型的值**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**并**D3DKMDT\_VPPS\_自定义**引入了 Windows 7 是存储在与图形处理单元 (GPU) 相关联的 CCD 连接数据库。 如果用户从一个 GPU 支持这些成员缩放到另一个 GPU 驱动程序与移动监视器，第二个 GPU 可能不受原始驱动程序。 在这种情况下操作系统将映射到系统的默认缩放这些缩放类型。

如果这两个 Gpu 支持的缩放类型**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**并**D3DKMDT\_VPPS\_自定义**，和驱动程序第一个 GPU 实现**D3DKMDT\_VPPS\_自定义**自定义缩放请求，然后如果监视器切换到第二个 GPU，为第二个 GPU 驱动程序将可能不知道如何将自定义的缩放请求的解释。 第二个的驱动程序应在这种情况下失败调用[ **DxgkDdiCommitVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559597)函数，并应返回**状态\_图形\_VIDPN\_模态\_不\_支持**状态代码; 操作系统将此缩放类型映射到系统的默认缩放。

 

 





