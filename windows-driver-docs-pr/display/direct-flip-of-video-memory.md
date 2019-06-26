---
title: 视频内存的直接交替
description: 直接翻页功能允许对组合模型的特殊优化以降低能耗。
ms.assetid: 00A8FCB1-966A-4176-9840-7EB5BA300C8B
keywords:
- 直接翻转
- DirectFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad4c2c2a319d744a82e40d20896e1ec80edbfbed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384876"
---
# <a name="direct-flip-of-video-memory"></a>视频内存的直接交替


直接翻页功能允许对组合模型的特殊优化以降低能耗。 优化都受益这些方案：

-   若要确保播放视频和其他全屏方案的最佳能源消耗，直接翻转使最少的内存带宽，以显示全屏幕内容，请确保全屏幕应用，其他应用和桌面之间平滑过渡环境。
-   用户想要查看的视频或运行的应用程序覆盖整个屏幕。 当用户进入或退出应用程序中，或通知的应用上出现时，无模式更改是必需的并体验非常顺利。 此外，用户喜欢在移动设备上的长的电池寿命，因为为全屏幕应用，如视频减少内存带宽需求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows 显示器驱动程序模型 (WDDM) 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现，完整的图形</td>
<td align="left">强制</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics...DirectFlip</strong></p></td>
</tr>
</tbody>
</table>

 

## <span id="directflip"></span><span id="DIRECTFLIP"></span>


## <a name="span-iddirectflipdevicedriverinterfaceddispanspan-iddirectflipdevicedriverinterfaceddispanspan-iddirectflipdevicedriverinterfaceddispandirectflip-device-driver-interface-ddi"></a><span id="DirectFlip_device_driver_interface__DDI_"></span><span id="directflip_device_driver_interface__ddi_"></span><span id="DIRECTFLIP_DEVICE_DRIVER_INTERFACE__DDI_"></span>DirectFlip 设备驱动程序接口 (DDI)


这些函数和结构是新的或更新 Windows 8:

-   [*CheckDirectFlipSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkdirectflipsupport)
-   [*CheckDirectFlipSupport(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkdirectflipsupport)
-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
-   [**D3D11\_1\_DDI\_CHECK\_DIRECT\_FLIP\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_check_direct_flip_flags)
-   [**D3DDDI\_CHECK\_DIRECT\_FLIP\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_check_direct_flip_flags)
-   [**D3DDDIARG\_CHECKDIRECTFLIPSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_checkdirectflipsupport)
-   [**D3DKMT\_DIRECTFLIP\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_directflip_support)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**D3DKMT\_WAITFORVERTICALBLANKEVENT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_waitforverticalblankevent2)
-   [**D3DKMTWaitForVerticalBlankEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforverticalblankevent2)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...DirectFlip**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





