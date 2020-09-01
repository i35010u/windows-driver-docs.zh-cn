---
title: 照片序列模式
description: 照片序列模式允许捕获一系列照片，以响应照相机的一次单击。
ms.assetid: 15F19FE1-6D09-4406-B096-E96D12BAF030
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec46531285afb7955057094202fb2c486d604684
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186101"
---
# <a name="photo-sequence-mode"></a>照片序列模式


照片序列模式允许捕获一系列照片，以响应照相机的一次单击。 在此模式下，捕获系统会持续将缓冲区发送到相机驱动程序以按顺序捕获照片。 此模式还允许在照片单击之前捕获某个时间段内的照片。

## <a name="photo-sequence-operation"></a>照片序列操作


如果能够序列化照片，照相机驱动程序支持 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOMODE**](./ksproperty-cameracontrol-extended-photomode.md) 控件。 捕获管道通过将 **KS \_ VideoControlFlag \_ StartPhotoSequenceCapture** 触发器发送到 photo stream 来启动照片序列。 此时，驱动程序必须开始发送捕获缓冲区。 捕获管道将通过向下发送 **KS \_ VideoControlFlag \_ StopPhotoSequenceCapture** 以触发照片流来停止照片序列。 对于每个已完成的照片，会向下发送一个新缓冲区，使其将帧捕获到。

捕获管道具有 "照片序列" 模式的配置阶段，在此阶段中，它将配置特定照片序列会话所需的过去帧的数目。 在配置阶段，驱动程序必须指定其支持的过去照片帧的最大数目。 同时，驱动程序将指定需要多少缓冲区才能支持所需数量的过去帧。

扩展控件 [**KSPROPERTY \_ CAMERACONTROL \_ extended \_ PHOTOTRIGGERTIME**](./ksproperty-cameracontrol-extended-phototriggertime.md)将向下传递用户在相机应用程序中单击 photo 触发器以获取照片序列的实际时间。 如果没有此时间，则驱动程序将不知道在 **KS \_ VideoControlFlag \_ StartPhotoSequenceCapture** 触发器到达后开始从哪个照片捕获返回帧的时间。 利用此控制，驱动程序应返回最靠近给定照片触发时间的照片。

## <a name="frame-count-negotiation"></a>帧计数协商


以下操作序列设置照相机驱动程序的照片模式和帧计数。

1.  应用程序调用 API 为照片序列捕获准备捕获系统和驱动程序。

2.  捕获系统会将对驱动程序的照片模式扩展属性请求（ [**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE**](./ksproperty-cameracontrol-extended-photomode.md) with KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ SEQUENCE）发送到标记中，以启动驱动程序到照片序列模式的转换。

    1.  从应用程序为驱动程序提供请求的历史记录帧计数。 驱动程序必须返回历史记录帧计数它能够支持以及保存历史记录帧所需的缓冲区数。

    2.  驱动程序必须使用 **KsEdit**通过照片序列模式转换调用来更新 pin 的分配器要求结构和缓冲区数。

    3.  该驱动程序会将其内部状态更改为照片序列模式。

3.  捕获系统会将 pin 转换为 KSSTATE \_ RUN，并为驱动程序提供针对照片序列模式请求的缓冲区数。

## <a name="control-support-requirements"></a>控制支持要求


照相机驱动程序支持照片序列模式需要以下扩展控件。

-   照片模式

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE**](./ksproperty-cameracontrol-extended-photomode.md)

-   照片帧速率

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOFRAMERATE**](./ksproperty-cameracontrol-extended-photoframerate.md)

-   最大照片帧速率

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMAXFRAMERATE**](./ksproperty-cameracontrol-extended-photomaxframerate.md)

-   照片触发时间

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOTRIGGERTIME**](./ksproperty-cameracontrol-extended-phototriggertime.md)

-   照片缩略图

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOTHUMBNAIL**](./ksproperty-cameracontrol-extended-photothumbnail.md)

-   最大视频帧速率

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ MAXVIDFPS \_ PHOTORES**](./ksproperty-cameracontrol-extended-maxvidfps-photores.md)

-   闪存模式 (支持 KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ SINGLEFLASH 功能) 

    Control： [ **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE**](./ksproperty-cameracontrol-extended-flashmode.md)

 

