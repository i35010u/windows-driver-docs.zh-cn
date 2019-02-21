---
title: Windows 8.1 的新 AVStream 接口
description: AVStream 流式处理媒体驱动程序接口进行了扩展，支持从 Windows 8.1 的新相机平台功能。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5757cf789163b01866878740c822b69456b8012f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534211"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 的新 AVStream 接口


AVStream 流式处理媒体驱动程序接口进行了扩展，支持从 Windows 8.1 的新相机平台功能。

## <a name="camera-platform"></a>照相机平台


从 Windows 8.1 扩展相机控件。 有关如何实现这些照相机控件的信息，请参阅下的主题[照相机控件属性](camera-control-properties.md)。

这些设备驱动程序接口 (DDIs) 支持这些扩展，是新的或更新：

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://msdn.microsoft.com/library/windows/hardware/dn567560)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567561)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://msdn.microsoft.com/library/windows/hardware/dn567562)
-   [**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://msdn.microsoft.com/library/windows/hardware/dn567566)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://msdn.microsoft.com/library/windows/hardware/dn567568)
-   [**KSEVENT\_VOLUMELIMIT\_已更改**](https://msdn.microsoft.com/library/windows/hardware/dn567569)
-   [KSPROPERTYSETID\_ExtendedCameraControl](https://msdn.microsoft.com/library/windows/hardware/dn567570) (包括这些属性:)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_CAMERAANGLEOFFSET**](https://msdn.microsoft.com/library/windows/hardware/dn567571)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567572)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567573)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FIELDOFVIEW**](https://msdn.microsoft.com/library/windows/hardware/dn567574)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567575)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567576)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_ISO**](https://msdn.microsoft.com/library/windows/hardware/dn567577)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_MAXVIDFPS\_PHOTORES**](https://msdn.microsoft.com/library/windows/hardware/dn567578)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_OPTIMIZATIONHINT**](https://msdn.microsoft.com/library/windows/hardware/dn567579)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567580)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567581)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567582)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**](https://msdn.microsoft.com/library/windows/hardware/dn567583)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME**](https://msdn.microsoft.com/library/windows/hardware/dn567584)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567585)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_TORCHMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567586)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_WARMSTART**](https://msdn.microsoft.com/library/windows/hardware/dn567587)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_WHITEBALANCEMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567588)
-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://msdn.microsoft.com/library/windows/hardware/dn567589)
-   [**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S** ](https://msdn.microsoft.com/library/windows/hardware/jj553707) (新**KSPROPERTY\_CAMERACONTROL\_图像\_PIN\_功能\_序列\_独占\_WITH\_记录**成员)
-   [**KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722) (新**标志**成员)
-   [**KSPROPERTY\_CAMERACONTROL\_区域\_OF\_感兴趣\_S** ](https://msdn.microsoft.com/library/windows/hardware/jj151592) (新**配置**成员)
-   [**KS\_VideoControlFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff567696) (新**KS\_VideoControlFlag\_StartPhotoSequenceCapture**并**KS\_VideoControlFlag\_StopPhotoSequenceCapture**常量值)
-   [**KS\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567645) (新**FrameCompletionNumber**成员)
-   请注意还额外[KSPROPERTYSETID\_ExtendedCameraControl](https://msdn.microsoft.com/library/windows/hardware/dn567570)属性设置中列出[视频捕获微型驱动程序属性集](https://msdn.microsoft.com/library/windows/hardware/ff568714)。

 

 




