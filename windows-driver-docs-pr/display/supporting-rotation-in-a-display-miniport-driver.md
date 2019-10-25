---
title: 在显示微型端口驱动程序中支持旋转
description: 在显示微型端口驱动程序中支持旋转
ms.assetid: 0c9bdd42-aeaf-4cc8-a979-9ed8eeda3811
keywords:
- 微型端口驱动程序 WDK 显示，旋转
- 旋转 WDK 显示
- 克隆模式 WDK 视频呈现网络
- surface 轮换 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1952a1eccfc39e79dcce8a1dd0b0f7dbcf1e6d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825603"
---
# <a name="supporting-rotation-in-a-display-miniport-driver"></a>在显示微型端口驱动程序中支持旋转


显示微型端口驱动程序的[**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)函数调用[**pfnUpdatePathSupportInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_updatepathsupportinfo)函数来报告视频显示网络（VidPN）拓扑中每个路径的旋转支持。 有关报告旋转支持的详细信息，请参阅[枚举 Cofunctional VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)。

Microsoft DirectX graphics 内核子系统使用非旋转曲面尺寸来创建共享主表面。 为了通知显示微型端口驱动程序旋转图面，DirectX 图形内核子系统指定了 D3DKMDT\_VIDPN\_在 D3DKMDT 的**循环**成员中[**提供\_路径\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)类型值[ **\_VIDPN\_存在\_路径\_转换**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_transformation)结构，该结构在[**D3DKMDT\_VIDPN\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)的**ContentTransformation**成员中指定\_调用显示微型端口驱动程序的[**DxgkDdiCommitVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)和[**DxgkDdiUpdateActiveVidPnPresentPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)函数。

**注意**   按逆时针方向定义所有旋转度数，这与 GDI 定义旋转的方式一致。

 

当 DirectX 子系统通知显示微型端口驱动程序旋转图面时，仅当在[**DXGKARG\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)结构的**Flags**成员中设置**旋转**位域标志时，驱动程序才应旋转 surface 数据*pPresent*参数在对驱动程序的[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)函数的调用中指向。 即使驱动程序确定屏幕的当前方向是从呈现数据进行旋转，并且未设置**旋转**，驱动程序也不应旋转数据。

### <a name="span-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanspan-idclone-mode_behaviorspanclone-mode-behavior"></a><span id="Clone-mode_behavior"></span><span id="clone-mode_behavior"></span><span id="CLONE-MODE_BEHAVIOR"></span>克隆模式行为

*克隆模式*是一种模式，在该模式下，视频现有源通过视频显示网络中的多个路径连接到多个视频显示目标。 （有关视频显示网络的详细信息，请参阅[多监视器和视频显示网络](multiple-monitors-and-video-present-networks.md)。）

显示微型端口驱动程序以不同的方式处理旋转，因为每个目标可能需要不同的旋转。 操作系统、各种版本的 Microsoft DirectX 运行时和用户模式客户端仅检测主视频显示目标的方向。 因此，视频显示源中的内容将始终与主视频显示目标的方向匹配。

下表显示了对于所有相关情况，显示微型端口驱动程序在克隆模式下的行为方式。 **旋转**标志的设置是[**DXGKARG\_当前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present)结构的**Flags**成员中的**旋转**位域的设置。

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
<td align="left"><p>即使未设置<strong>旋转</strong>标志，驱动程序也将旋转辅助目标。</p></td>
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
<td align="left"><p>由于未设置<strong>旋转</strong>，驱动程序不会旋转主目标。 由于辅助目标与源中内容的方向不匹配，因此驱动程序必须旋转辅助目标。</p>
<p>当客户端是旋转感知型，并且它已正确定向源内容时，会发生这种情况。 因此，操作系统不会设置<strong>旋转</strong>。</p></td>
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

 

## <a name="span-idclone-mode_requirementsspanspan-idclone-mode_requirementsspanclone-mode-requirements-starting-with-windows81-update"></a><span id="clone-mode_requirements"></span><span id="CLONE-MODE_REQUIREMENTS"></span>从 Windows 8.1 更新开始的克隆模式要求


从 Windows 8.1 更新开始，驱动程序必须满足这些要求。 如果启用了测试签名，则如果驱动程序无法满足这些要求，则会发生系统错误检查。

<span id="Primary_clone_path"></span><span id="primary_clone_path"></span><span id="PRIMARY_CLONE_PATH"></span>*主要克隆路径*  
**定义：** 包含复制源显示的目标监视器的路径，例如，在便携式计算机上复制显示的外部监视器。

**要求：** 在主克隆路径中，驱动程序必须将**Offset0**设置**为 TRUE** ，D3DKMDT\_\_VIDPN 中的其他3个偏移量值[ **\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)为**FALSE**。

对于纵向第一次源显示，主克隆路径不 rotationally 偏移。 这意味着主要克隆路径的偏移量始终为零（[**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset0**为**TRUE**），并且桌面窗口管理器（DWM）提前旋转其内容以匹配正确的方向。

主克隆路径确定所有主和辅助克隆目标的监视器刷新频率。

<span id="Secondary_clone_path"></span><span id="secondary_clone_path"></span><span id="SECONDARY_CLONE_PATH"></span>*辅助克隆路径*  
**定义：** 包含任何其他目标监视器的路径，这些监视器还不包含在源显示中的副本。

**要求：** 在辅助克隆路径中，驱动程序必须在 D3DKMDT\_VIDPN\_存在的4个偏移值中至少有一个值[ **\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)为**TRUE**。 如果驱动程序不支持与路径无关的旋转，则应在所有辅助克隆路径中将**Offset0**设置为**TRUE** 。

下面是驱动程序在支持与路径无关的旋转时应进行的两个设置的示例：

<span id="Landscape-first_example"></span><span id="landscape-first_example"></span><span id="LANDSCAPE-FIRST_EXAMPLE"></span>**横向-第一个示例**  
如果辅助克隆路径中的源显示和目标均为横向辅助克隆路径，则驱动程序会将[**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset0**为**TRUE** ，而 D3DKMDT 中的其他3个偏移值 **\_VIDPN\_提供\_路径\_旋转\_支持**为**FALSE**。 在这种情况下，在辅助克隆路径中，驱动程序会将**Offset0**和**Offset180**都设置为**TRUE** ，将其他偏移值设置为**FALSE**。

<span id="Portrait-first_example"></span><span id="portrait-first_example"></span><span id="PORTRAIT-FIRST_EXAMPLE"></span>**纵向-第一个示例**  
如果源显示为纵向第一台设备并连接到第一个二级外部监视器，则该驱动程序会将**Offset270**或**Offset90**设置为**TRUE**。

有关详细信息，请参阅[支持与路径无关的旋转](supporting-path-independent-rotation.md)。

 

 





