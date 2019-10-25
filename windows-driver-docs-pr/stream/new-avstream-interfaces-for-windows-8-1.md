---
title: Windows 8.1 的新 AVStream 接口
description: AVStream 流媒体驱动程序接口已扩展为支持从 Windows 8.1 开始的新相机平台功能。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: e5feb7427274586d850a539a22f41ca5551ff450
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823593"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 的新 AVStream 接口


AVStream 流媒体驱动程序接口已扩展为支持从 Windows 8.1 开始的新相机平台功能。

## <a name="camera-platform"></a>照相机平台


照相机控件从 Windows 8.1 开始扩展。 有关如何实现这些相机控件的信息，请参阅[相机控制属性](camera-control-properties.md)下的主题。

这些设备驱动程序接口（DDIs）支持这些扩展，并且是新的或更新的：

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)
-   [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-volumelimit)
-   [**KSEVENT\_VOLUMELIMIT\_更改**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-volumelimit-changed)
-   [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol) （包括以下属性：）
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_CAMERAANGLEOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_ISO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_MAXVIDFPS\_PHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)
    -   [**KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)
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
-   [**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s) （new **KSPROPERTY\_CAMERACONTROL\_\_\_PIN\_\_@no__包含\_记录成员的 t_14_** ）
-   [**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) （新**标志**成员）
-   [**KSPROPERTY\_CAMERACONTROL\_地区\_\_兴趣\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s) （新**配置**成员）
-   [**KS\_VideoControlFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_videocontrolflags) （new **KS\_VideoControlFlag\_StartPhotoSequenceCapture** and **KS\_VideoControlFlag\_StopPhotoSequenceCapture**常量值）
-   [**KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)（new **FrameCompletionNumber**成员）
-   另请注意， [\_KSPROPERTYSETID ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)属性集在[视频捕获微型驱动程序属性](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-minidriver-property-sets)集中列出。

 

 




