---
title: Windows 8.1 的新 AVStream 接口
description: AVStream 流媒体驱动程序接口已扩展为支持从 Windows 8.1 开始的新相机平台功能。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: d814eb3d66b3b344915a074fbde1147d250e5f23
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192147"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 的新 AVStream 接口


AVStream 流媒体驱动程序接口已扩展为支持从 Windows 8.1 开始的新相机平台功能。

## <a name="camera-platform"></a>照相机平台


照相机控件从 Windows 8.1 开始扩展。 有关如何实现这些相机控件的信息，请参阅 [相机控制属性](camera-control-properties.md)下的主题。

这些设备驱动程序接口 (DDIs) 支持这些扩展，并且是新的或更新的：

-   [**KSCAMERA \_ EXTENDEDPROP \_ CAMERAOFFSET**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
-   [**KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)
-   [**KSCAMERA \_ EXTENDEDPROP \_ FIELDOFVIEW**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)
-   [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA \_ MAXVIDEOFPS \_ FORPHOTORES**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID \_ VolumeLimit](./kseventsetid-volumelimit.md)
-   [**KSEVENT \_ VOLUMELIMIT \_ 已更改**](./ksevent-volumelimit-changed.md)
-   [KSPROPERTYSETID \_ExtendedCameraControl](./kspropertysetid-extendedcameracontrol.md) (包括以下属性： ) 
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ CAMERAANGLEOFFSET**](./ksproperty-cameracontrol-extended-cameraangleoffset.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EVCOMPENSATION**](./ksproperty-cameracontrol-extended-evcompensation.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EXPOSUREMODE**](./ksproperty-cameracontrol-extended-exposuremode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FIELDOFVIEW**](./ksproperty-cameracontrol-extended-fieldofview.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FLASHMODE**](./ksproperty-cameracontrol-extended-flashmode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSMODE**](./ksproperty-cameracontrol-extended-focusmode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ISO**](./ksproperty-cameracontrol-extended-iso.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ MAXVIDFPS \_ PHOTORES**](./ksproperty-cameracontrol-extended-maxvidfps-photores.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT**](./ksproperty-cameracontrol-extended-optimizationhint.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOFRAMERATE**](./ksproperty-cameracontrol-extended-photoframerate.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOMAXFRAMERATE**](./ksproperty-cameracontrol-extended-photomaxframerate.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOMODE**](./ksproperty-cameracontrol-extended-photomode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTHUMBNAIL**](./ksproperty-cameracontrol-extended-photothumbnail.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTRIGGERTIME**](./ksproperty-cameracontrol-extended-phototriggertime.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ SCENEMODE**](./ksproperty-cameracontrol-extended-scenemode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ TORCHMODE**](./ksproperty-cameracontrol-extended-torchmode.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ WARMSTART**](./ksproperty-cameracontrol-extended-warmstart.md)
    -   [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ WHITEBALANCEMODE**](./ksproperty-cameracontrol-extended-whitebalancemode.md)
-   [**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2**](./ksproperty-pin-proposedataformat2.md)
-   [**KSPROPERTY \_CAMERACONTROL \_ 图像 \_ pin \_ 功能 \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s) (新 **的 KSPROPERTY \_ CAMERACONTROL \_ 图像 \_ pin \_ 功能 \_ 序列 \_ \_ 与 \_ 记录** 成员) 
-   [**KSP \_固定**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) (新 **标志** 成员) 
-   [**KSPROPERTY \_CAMERACONTROL \_ \_ \_ 感兴趣的 \_ 区域**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s) (新的 **配置** 成员) 
-   [**KS \_VideoControlFlags**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_videocontrolflags) (New **KS \_ VideoControlFlag \_ StartPhotoSequenceCapture** 和 **KS \_ VideoControlFlag \_ StopPhotoSequenceCapture** 常量值) 
-   [**KS \_框架 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) (new **FrameCompletionNumber** 成员) 
-   另请注意，[视频捕获微型驱动程序属性](./video-capture-minidriver-property-sets.md)集中列出了其他[KSPROPERTYSETID \_ ExtendedCameraControl](./kspropertysetid-extendedcameracontrol.md)属性集。

 

