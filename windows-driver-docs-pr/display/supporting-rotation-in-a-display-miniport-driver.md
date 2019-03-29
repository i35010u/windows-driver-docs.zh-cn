---
title: 在显示微型端口驱动程序中支持旋转
description: 在显示微型端口驱动程序中支持旋转
ms.assetid: 0c9bdd42-aeaf-4cc8-a979-9ed8eeda3811
keywords:
- 微型端口驱动程序 WDK 显示旋转
- 旋转 WDK 显示
- 克隆模式 WDK 视频存在网络
- 图面上旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171bc23d8d25dadb2d4106d65edb61676d17c422
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576256"
---
# <a name="supporting-rotation-in-a-display-miniport-driver"></a>在显示微型端口驱动程序中支持旋转


显示微型端口驱动程序的[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649)函数调用[ **pfnUpdatePathSupportInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562106)函数支持报告，旋转的视频的存在 (VidPN) 网络拓扑中每个路径。 有关报告旋转支持的详细信息，请参阅[枚举同时正常工作 VidPN 源和目标模式](enumerating-cofunctional-vidpn-source-and-target-modes.md)。

Microsoft DirectX 图形内核子系统使用非旋转图面上的维度来创建共享主图面。 若要通知显示微型端口驱动程序，即可旋转图面，DirectX 图形内核子系统指定[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转**](https://msdn.microsoft.com/library/windows/hardware/ff546700)的类型化中的值**旋转**的成员[ **D3DKMDT\_VIDPN\_存在\_路径\_转换**](https://msdn.microsoft.com/library/windows/hardware/ff546719)中指定的结构**ContentTransformation**的成员[ **D3DKMDT\_VIDPN\_存在\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff546647)对显示微型端口驱动程序的调用中的结构[ **DxgkDdiCommitVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559597)和[ **DxgkDdiUpdateActiveVidPnPresentPath** ](https://msdn.microsoft.com/library/windows/hardware/ff560803)函数。

**请注意**  逆时针方向与 GDI 如何定义旋转一致中定义所有的旋转度。

 

当 DirectX 子系统通知时显示微型端口驱动程序来旋转图面时，该驱动程序应旋转图面上的数据才**旋转**在中设置了位域标志**标志**成员[**DXGKARG\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff557618)结构的*pPresent*参数，驱动程序的调用中指向[ **DxgkDdiPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff559743)函数。 即使该驱动程序确定当前屏幕的方向从演示数据旋转并**旋转**不可设置，该驱动程序不应轮换数据。

### <a name="span-idclone-modebehaviorspanspan-idclone-modebehaviorspanspan-idclone-modebehaviorspanclone-mode-behavior"></a><span id="Clone-mode_behavior"></span><span id="clone-mode_behavior"></span><span id="CLONE-MODE_BEHAVIOR"></span>克隆模式行为

*克隆模式*是视频显示源连接到多个视频的显示目标通过视频存在网络中的多个路径模式。 (有关视频存在网络的详细信息，请参阅[多个监视器和视频存在网络](multiple-monitors-and-video-present-networks.md)。)

如果它会因为每个目标可能需要不同的旋转在克隆模式下运行，显示微型端口驱动程序将以不同方式处理旋转。 操作系统，各种版本的 Microsoft DirectX 运行时和用户模式下客户端检测仅主视频的显示目标的方向。 因此，视频显示源中的内容将始终匹配主视频的显示目标的方向。

下表显示了显示微型端口驱动程序在所有相关的情况下的克隆模式下的行为方式。 设置**旋转**标志是设置**旋转**中的位域**标志**隶属[ **DXGKARG\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff557618)结构。

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
<td align="left"><p>该驱动程序执行没有旋转。</p></td>
</tr>
<tr class="even">
<td align="left"><p>不旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>该驱动程序将旋转辅助目标，即使<strong>旋转</strong>未设置标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旋转</p></td>
<td align="left"><p>不旋转</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>该驱动程序会旋转的主要目标而不是辅助目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>旋转</p></td>
<td align="left"><p>不旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>因为<strong>旋转</strong>未设置，该驱动程序不会不会旋转的主要目标。 辅助目标与源中的内容的方向不匹配，因为该驱动程序必须旋转辅助目标。</p>
<p>当客户端是旋转感知并按已它具有正确方向源的内容时，将出现这种情况。 因此，未设置操作系统不会<strong>旋转</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>该驱动程序会旋转的主要和辅助目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>旋转</p></td>
<td align="left"><p>旋转</p></td>
<td align="left"><p>未设置</p></td>
<td align="left"><p>旋转感知客户端具有已正确面向源的内容。 因此，没有其他旋转是必需的。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idclone-moderequirementsspanspan-idclone-moderequirementsspanclone-mode-requirements-starting-with-windows81-update"></a><span id="clone-mode_requirements"></span><span id="CLONE-MODE_REQUIREMENTS"></span>从 Windows 8.1 更新开始克隆模式要求


从 Windows 8.1 更新开始，驱动程序必须满足这些要求。 如果已启用测试签名，如果驱动程序不能满足这些要求，将发生系统错误检查。

<span id="Primary_clone_path"></span><span id="primary_clone_path"></span><span id="PRIMARY_CLONE_PATH"></span>*主要克隆路径*  
**定义：** 包括的目标监视器的重复项的源显示的路径 — 例如，外部监视器的重复项的便携式计算机上显示。

**要求：** 在主克隆路径中，该驱动程序必须设置**Offset0**到**TRUE**和其他 3 个偏移量中的值[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)到**FALSE**。

对于纵向第一个源显示主克隆路径是不旋转的偏移量。 这意味着主克隆路径始终具有偏移量为零 ([**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705).**Offset0**是**TRUE**)，并桌面窗口管理器 (DWM) 将其内容预先以匹配正确的方向旋转。

主要克隆路径将确定监视器的刷新频率的所有主要和辅助克隆目标。

<span id="Secondary_clone_path"></span><span id="secondary_clone_path"></span><span id="SECONDARY_CLONE_PATH"></span>*辅助克隆路径*  
**定义：** 包括任何其他目标监视器、 不属于主要克隆路径，也可以复制源显示的路径。

**要求：** 在辅助克隆路径中，该驱动程序必须设置至少一个中的 4 个偏移量值[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)到 **，则返回 TRUE**。 如果该驱动程序不支持独立于路径的旋转，则应设置**Offset0**到**TRUE**在所有辅助克隆路径中。

下面是如果它支持独立于路径的旋转，应使该驱动程序的设置的两个示例：

<span id="Landscape-first_example"></span><span id="landscape-first_example"></span><span id="LANDSCAPE-FIRST_EXAMPLE"></span>**横向第一个示例**  
如果源显示和辅助克隆路径中的目标是这两个横向第一个监视器，辅助克隆路径中的驱动程序会将设置[ **D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**](https://msdn.microsoft.com/library/windows/hardware/ff546705)。**Offset0**到**TRUE**和其他 3 个偏移量中的值**D3DKMDT\_VIDPN\_存在\_路径\_旋转\_支持**到**FALSE**。 或者在这种情况下，辅助克隆路径中的驱动程序会同时设置**Offset0**并**Offset180**到**TRUE**和其他偏移量值添加到**FALSE**.

<span id="Portrait-first_example"></span><span id="portrait-first_example"></span><span id="PORTRAIT-FIRST_EXAMPLE"></span>**纵向第一个示例**  
如果源显示纵向第一个设备，以及连接到横向第一个外部监视器，辅助克隆路径中的驱动程序会设置**Offset270**或**Offset90**到**TRUE**。

有关详细信息，请参阅[支持独立于路径的旋转](supporting-path-independent-rotation.md)。

 

 





