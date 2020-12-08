---
title: 在显示微型端口驱动程序中支持旋转
description: 在显示微型端口驱动程序中支持旋转
keywords:
- 微型端口驱动程序 WDK 显示，旋转
- 旋转 WDK 显示
- 克隆模式 WDK 视频呈现网络
- surface 轮换 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4620997b2dd88ae7ccc8a328076e67878ee4caa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838987"
---
# <a name="supporting-rotation-in-a-display-miniport-driver"></a>在显示微型端口驱动程序中支持旋转


显示微型端口驱动程序的 [**DxgkDdiEnumVidPnCofuncModality**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality) 函数将调用 [**pfnUpdatePathSupportInfo**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_updatepathsupportinfo) 函数来报告视频呈现网络 (VidPN) 拓扑中每个路径的旋转支持。 有关报告旋转支持的详细信息，请参阅 [枚举 Cofunctional VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)。

Microsoft DirectX graphics 内核子系统使用非旋转曲面尺寸来创建共享主表面。 为了通知显示微型端口驱动程序旋转图面，DirectX 图形内核子系统在 [**D3DKMDT vidpn 显示路径 \_ \_ \_ \_ 转换**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_transformation)结构的 **旋转** 成员中指定 [**D3DKMDT vidpn 显示路径 \_ \_ \_ \_ 旋转**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)类型值，该结构是在调用显示微型端口驱动程序的 [**DxgkDdiCommitVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)和 [**DxgkDdiUpdateActiveVidPnPresentPath**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)函数的 [**D3DKMDT \_ vidpn \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)显示路径结构的 **ContentTransformation** 成员中指定的。

**注意**   所有旋转度数都按逆时针方向定义，这与 GDI 定义旋转的方式一致。

 

当 DirectX 子系统通知显示微型端口驱动程序旋转图面时，只有在 *pPresent* 参数在调用驱动程序的 [**DxgkDdiPresent**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)函数的调用中所指向的 [**\_ DXGKARG**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)的 **flags** 成员中设置了 **旋转** 位域标志时，驱动程序才应该旋转图面数据。 即使驱动程序确定屏幕的当前方向是从呈现数据进行旋转，并且未设置 **旋转** ，驱动程序也不应旋转数据。

### <a name="span-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanclone-mode-behavior"></a><span id="Clone-mode_behavior"></span><span id="clone-mode_behavior"></span><span id="CLONE-MODE_BEHAVIOR"></span>克隆模式行为

*克隆模式* 是一种模式，在该模式下，视频现有源通过视频显示网络中的多个路径连接到多个视频显示目标。  (有关视频显示网络的详细信息，请参阅 [多监视器和视频显示网络](multiple-monitors-and-video-present-networks.md)。 ) 

显示微型端口驱动程序以不同的方式处理旋转，因为每个目标可能需要不同的旋转。 操作系统、各种版本的 Microsoft DirectX 运行时和用户模式客户端仅检测主视频显示目标的方向。 因此，视频显示源中的内容将始终与主视频显示目标的方向匹配。

下表显示了对于所有相关情况，显示微型端口驱动程序在克隆模式下的行为方式。 **旋转** 标志的设置是 [**DXGKARG \_ 存在**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)结构的 **Flags** 成员中的 **旋转** 位域的设置。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主目标</th>
<th align="left">辅助目标</th>
<th align="left">旋转标志</th>
<th align="left">驱动程序行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>不旋转</p></td>
<td align="left"><p>不旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>驱动程序不执行旋转。</p></td>
</tr>
<tr class="even">
<td align="left"><p>不旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>即使未设置 <strong>旋转</strong> 标志，驱动程序也将旋转辅助目标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旋转</p></td>
<td align="left"><p>不旋转</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>驱动程序将旋转主目标，而不是辅助目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>旋转</p></td>
<td align="left"><p>不旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>由于未设置 <strong>旋转</strong> ，驱动程序不会旋转主目标。 由于辅助目标与源中内容的方向不匹配，因此驱动程序必须旋转辅助目标。</p>
<p>当客户端是旋转感知型，并且它已正确定向源内容时，会发生这种情况。 因此，操作系统不会设置 <strong>旋转</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>驱动程序会旋转主目标和辅助目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>旋转感知客户端已正确定向源的内容。 因此，不需要进行其他旋转。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idclone-mode_requirementsspanspan-idclone-mode_requirementsspanclone-mode-requirements-starting-with-windows-81-update"></a><span id="clone-mode_requirements"></span><span id="CLONE-MODE_REQUIREMENTS"></span>从 Windows 8.1 更新开始的克隆模式要求


从 Windows 8.1 更新开始，驱动程序必须满足这些要求。 如果启用了测试签名，则如果驱动程序无法满足这些要求，则会发生系统错误检查。

<span id="Primary_clone_path"></span><span id="primary_clone_path"></span><span id="PRIMARY_CLONE_PATH"></span>*主要克隆路径*  
**定义：** 包含复制源显示的目标监视器的路径，例如，在便携式计算机上复制显示的外部监视器。

**要求：** 在主克隆路径中，驱动程序必须将 **Offset0** 设置为 **TRUE** ，并将 [**D3DKMDT VIDPN 中的 \_ \_ \_ \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support) 其他3个偏移量值设置为 **FALSE**。

对于纵向第一次源显示，主克隆路径不 rotationally 偏移。 这意味着主要克隆路径的偏移量始终为零 ([**D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 旋转 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset0**) **，** 桌面窗口管理器 (DWM) 会提前旋转其内容以匹配正确的方向。

主克隆路径确定所有主和辅助克隆目标的监视器刷新频率。

<span id="Secondary_clone_path"></span><span id="secondary_clone_path"></span><span id="SECONDARY_CLONE_PATH"></span>*辅助克隆路径*  
**定义：** 包含任何其他目标监视器的路径，这些监视器还不包含在源显示中的副本。

**要求：** 在辅助克隆路径中，驱动程序必须在 [**D3DKMDT VIDPN 中至少设置4个 \_ \_ \_ \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)偏移量值 **之一。** 如果驱动程序不支持与路径无关的旋转，则应在所有辅助克隆路径中将 **Offset0** 设置为 **TRUE** 。

下面是驱动程序在支持与路径无关的旋转时应进行的两个设置的示例：

<span id="Landscape-first_example"></span><span id="landscape-first_example"></span><span id="LANDSCAPE-FIRST_EXAMPLE"></span>**横向-第一个示例**  
如果源显示和辅助克隆路径中的目标都是横向的监视器，则该驱动程序将设置 [**D3DKMDT \_ VIDPN \_ 显示 \_ 路径 \_ 旋转 \_ 支持**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset0** 为 **TRUE** ，而 D3DKMDT VIDPN 中的其他3个偏移量值提供对 **FALSE** 的 **\_ \_ \_ 路径 \_ 旋转 \_ 支持**。 在这种情况下，在辅助克隆路径中，驱动程序会将 **Offset0** 和 **Offset180** 都设置为 **TRUE** ，将其他偏移值设置为 **FALSE**。

<span id="Portrait-first_example"></span><span id="portrait-first_example"></span><span id="PORTRAIT-FIRST_EXAMPLE"></span>**纵向-第一个示例**  
如果源显示为纵向第一台设备并连接到第一个二级外部监视器，则该驱动程序会将 **Offset270** 或 **Offset90** 设置为 **TRUE**。

有关详细信息，请参阅 [支持 Path-Independent 旋转](supporting-path-independent-rotation.md)。

 

