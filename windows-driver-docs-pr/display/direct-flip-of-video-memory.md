---
title: 视频内存的直接交替
description: 直接翻转功能允许对组合模型进行特殊优化，以减少功率消耗。
ms.assetid: 00A8FCB1-966A-4176-9840-7EB5BA300C8B
keywords:
- 直接翻转
- DirectFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aedd3fc4a28465732a29082621b0010330bb608
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103926"
---
# <a name="direct-flip-of-video-memory"></a>视频内存的直接交替


直接翻转功能允许对组合模型进行特殊优化，以减少功率消耗。 这些方案的优化优点如下：

-   为了确保视频播放和其他全屏方案的最佳功率消耗，直接翻转启用了最少的内存带宽来显示全屏内容，并确保全屏应用、其他应用和桌面环境之间的平滑转换。
-   用户希望观看视频或运行涵盖整个屏幕的应用。 当用户进入或退出应用程序，或在应用上出现通知时，无需更改模式，并且体验会平稳。 而且，用户喜欢在移动设备上延长电池寿命，因为全屏应用（如视频）的内存带宽需求会有所减少。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 Windows 显示器驱动程序模型 (WDDM) 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-完整图形</td>
<td align="left">必需</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>¦ DirectFlip</strong></p></td>
</tr>
</tbody>
</table>

 

## <span id="directflip"></span><span id="DIRECTFLIP"></span>


## <a name="span-iddirectflip_device_driver_interface__ddi_spanspan-iddirectflip_device_driver_interface__ddi_spanspan-iddirectflip_device_driver_interface__ddi_spandirectflip-device-driver-interface-ddi"></a><span id="DirectFlip_device_driver_interface__DDI_"></span><span id="directflip_device_driver_interface__ddi_"></span><span id="DIRECTFLIP_DEVICE_DRIVER_INTERFACE__DDI_"></span>DirectFlip 设备驱动程序接口 (DDI) 


这些函数和结构是适用于 Windows 8 的新功能或更新的：

-   [*CheckDirectFlipSupport*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkdirectflipsupport)
-   [*CheckDirectFlipSupport (D3D11 \_ 1) *](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkdirectflipsupport)
-   [*DxgkDdiSetVidPnSourceAddress*](/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
-   [**D3D11 \_ 1 \_ DDI \_ CHECK \_ 直接 \_ 翻转 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_check_direct_flip_flags)
-   [**D3DDDI \_ 检查 \_ 直接 \_ 翻转 \_ 标志**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_check_direct_flip_flags)
-   [**D3DDDIARG \_ CHECKDIRECTFLIPSUPPORT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_checkdirectflipsupport)
-   [**D3DKMT \_ DIRECTFLIP \_ 支持**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_directflip_support)
-   [**D3DKMT \_ QUERYADAPTERINFO**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**D3DKMT \_ WAITFORVERTICALBLANKEVENT2**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_waitforverticalblankevent2)
-   [**D3DKMTWaitForVerticalBlankEvent2**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforverticalblankevent2)
-   [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK \_ SEGMENTFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)
-   [**DXGK \_ SETVIDPNSOURCEADDRESS \_ 标志**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) ，了解 **¦ DirectFlip**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

