---
title: 多平面覆盖 VidPN 呈现
description: 适用于用于在多个图面上呈现的函数的要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cf0bd4a29ee5666f90d199b4d2a774119b5e0d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816321"
---
# <a name="multiplane-overlay-vidpn-presentation"></a>多平面覆盖 VidPN 呈现


使用 multiplane 叠加时，这些要求适用于在视频现有网络中的多个表面上呈现的函数 (VidPNs) ：

<span id="DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay"></span><span id="dxgkddisetvidpnsourceaddresswithmultiplaneoverlay"></span><span id="DXGKDDISETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY"></span>[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)  
-   如果 [**DXGK \_ MULTIPLANE \_ 叠加 \_ 平面**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)。**Enabled** 为 false，则显示微型端口驱动程序应禁用指定的平面。
-   如果在之前对 [*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay) 的调用中启用了平面，但当前调用中不存在该平面，则驱动程序应继续显示该平面而不进行翻转。
-   该驱动程序有可能会在同一 VSync 中收到多个对 [*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay) 的调用， (一次调用翻转一个平面，另一个调用将不同的平面翻转) 。 在这种情况下，驱动程序应同时处理两个调用。
-   传递的数据应在用户模式下由受信任的源进行验证。 但是，显示微型端口驱动程序仍应检查数据，以确保它不会导致问题。 如果数据不正确，则驱动程序可以使用 **状态 " \_ 无效 \_ 参数** " 错误代码来使调用失败，但这种失败可能不会正常处理，而是指操作系统或用户模式驱动程序中的 bug。

<span id="DxgkDdiSetVidPnSourceVisibility"></span><span id="dxgkddisetvidpnsourcevisibility"></span><span id="DXGKDDISETVIDPNSOURCEVISIBILITY"></span>[*DxgkDdiSetVidPnSourceVisibility*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)  
[**DXGKARG \_ SETVIDPNSOURCEVISIBILITY**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。**Visible** 在对此函数的调用中，在给定源上，"可见" 设置为 " **FALSE** "，则必须禁用所有硬件平面，其中包括用于主表面的层。 如果 " **可见** " 设置为 " **TRUE**"，则只需启用用于主表面的平面，所有其他平面都必须保持禁用状态。

<span id="DxgkDdiSetVidPnSourceAddress"></span><span id="dxgkddisetvidpnsourceaddress"></span><span id="DXGKDDISETVIDPNSOURCEADDRESS"></span>[*DxgkDdiSetVidPnSourceAddress*](/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))  
调用此函数时，驱动程序应禁用所有非主要覆盖面。 在 multiplane 叠加模式下，将使用 [*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay) 翻转主图面。

 

