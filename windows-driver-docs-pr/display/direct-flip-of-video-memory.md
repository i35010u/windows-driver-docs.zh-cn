---
title: 视频内存的直接交替
description: 直接翻页功能允许对组合模型的特殊优化以降低能耗。
ms.assetid: 00A8FCB1-966A-4176-9840-7EB5BA300C8B
keywords:
- 直接翻转
- DirectFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bad5a4c159c2b963bf8a3a50d16331afd7396e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342429"
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

-   [*CheckDirectFlipSupport*](https://msdn.microsoft.com/library/windows/hardware/hh698234)
-   [*CheckDirectFlipSupport(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh406253)
-   [*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)
-   [**D3D11\_1\_DDI\_CHECK\_DIRECT\_FLIP\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/hh451044)
-   [**D3DDDI\_CHECK\_DIRECT\_FLIP\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/hh451172)
-   [**D3DDDIARG\_CHECKDIRECTFLIPSUPPORT**](https://msdn.microsoft.com/library/windows/hardware/hh451072)
-   [**D3DKMT\_DIRECTFLIP\_支持**](https://msdn.microsoft.com/library/windows/hardware/hh406459)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://msdn.microsoft.com/library/windows/hardware/ff548203)
-   [**D3DKMT\_WAITFORVERTICALBLANKEVENT2**](https://msdn.microsoft.com/library/windows/hardware/hh780272)
-   [**D3DKMTWaitForVerticalBlankEvent2**](https://msdn.microsoft.com/library/windows/hardware/hh780252)
-   [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)
-   [**DXGK\_SEGMENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562039)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562052)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...DirectFlip**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





