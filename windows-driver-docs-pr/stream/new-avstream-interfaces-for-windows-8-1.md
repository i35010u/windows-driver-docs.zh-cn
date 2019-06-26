---
title: Windows 8.1 的新 AVStream 接口
description: AVStream 流式处理媒体驱动程序接口进行了扩展，支持从 Windows 8.1 的新相机平台功能。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: a993e9c969075cf6d771bd7f5ad410d80ba1942f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363276"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 的新 AVStream 接口


AVStream 流式处理媒体驱动程序接口进行了扩展，支持从 Windows 8.1 的新相机平台功能。

## <a name="camera-platform"></a>照相机平台


从 Windows 8.1 扩展相机控件。 有关如何实现这些照相机控件的信息，请参阅下的主题[照相机控件属性](camera-control-properties.md)。

这些设备驱动程序接口 (DDIs) 支持这些扩展，是新的或更新：

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)
-   [**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-volumelimit)
-   [**KSEVENT\_VOLUMELIMIT\_已更改**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-volumelimit-changed)
-   [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol) (包括这些属性:)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_CAMERAANGLEOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_ISO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_MAXVIDFPS\_PHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)
    -   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_OPTIMIZATIONHINT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_TORCHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_WARMSTART**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_WHITEBALANCEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode)
-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat2)
-   [**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s) (新**KSPROPERTY\_CAMERACONTROL\_图像\_PIN\_功能\_序列\_独占\_WITH\_记录**成员)
-   [**KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin) (新**标志**成员)
-   [**KSPROPERTY\_CAMERACONTROL\_区域\_OF\_感兴趣\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s) (新**配置**成员)
-   [**KS\_VideoControlFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_videocontrolflags) (新**KS\_VideoControlFlag\_StartPhotoSequenceCapture**并**KS\_VideoControlFlag\_StopPhotoSequenceCapture**常量值)
-   [**KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info) (新**FrameCompletionNumber**成员)
-   请注意还额外[KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)属性设置中列出[视频捕获微型驱动程序属性集](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-minidriver-property-sets)。

 

 




