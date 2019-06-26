---
title: 照片序列模式
description: 照片序列模式使捕获照片的照相机张照片单击操作的响应中的序列。
ms.assetid: 15F19FE1-6D09-4406-B096-E96D12BAF030
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 759e138f5782624c5c219caf1dac98e1fbb05a95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383500"
---
# <a name="photo-sequence-mode"></a>照片序列模式


照片序列模式使捕获照片的照相机张照片单击操作的响应中的序列。 在此模式下，捕获系统不断将缓冲区发送到要捕获序列中的照片的照相机驱动程序。 此模式还允许从照片单击之前的时间段中拍照。

## <a name="photo-sequence-operation"></a>照片序列操作


照相机驱动程序支持[ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)控制如果能够序列化的照片。 捕获管道首先会向下发送照片序列**KS\_VideoControlFlag\_StartPhotoSequenceCapture**照片流的触发器。 此时，驱动程序必须开始发送捕获缓冲区。 捕获管道将通过向下发送停止照片序列**KS\_VideoControlFlag\_StopPhotoSequenceCapture**来触发照片流。 为已完成的每张照片，新的缓冲区是发送给它捕获到的帧的驱动程序。

捕获管道不包含在此期间它将配置过去帧所需的特定照片序列会话数的照片序列模式配置阶段。 在配置阶段中，该驱动程序必须指定过去的照片帧，它支持的最大数目。 此外，驱动程序将指定数量的缓冲区所需支持所需的过去的帧数。

扩展的控件[ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)，将通过用户单击照片触发器实际时间在采取照片序列的相机应用程序。 没有这一次的情况下，驱动程序不会知道捕获开始时返回的帧的照片**KS\_VideoControlFlag\_StartPhotoSequenceCapture**触发器到达。 与此控件，该驱动程序应返回与给定的照片触发器时间最接近的照片。

## <a name="frame-count-negotiation"></a>帧计数协商


以下一系列操作以照相机的驱动程序设置的照片模式和帧计数。

1.  应用程序调用一个 API，用于为照片序列捕获准备捕获系统和驱动程序。

2.  捕获系统将调用照片模式扩展的属性请求发送到该驱动程序， [ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)与KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_设置标志，在启动的驱动程序添加到照片序列模式转换的序列。

    1.  该驱动程序从应用程序提供了请求的历史记录的帧数。 驱动程序必须返回历史记录帧数能够支持的缓冲区数以及所需的保留的历史记录帧。

    2.  该驱动程序必须使用的照片序列模式转换调用使用的缓冲区数更新 pin 的分配器要求结构**KsEdit**。

    3.  该驱动程序将其内部状态更改为照片序列模式。

3.  捕获系统将转换到 KSSTATE pin\_运行并为该驱动程序提供的照片序列模式为请求的缓冲区数。

## <a name="control-support-requirements"></a>控件支持要求


照相机的驱动程序以支持照片序列模式需要对以下扩展控件的支持。

-   照片模式

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)

-   照片帧速率

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)

-   照片的最大帧速率

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)

-   照片触发时间

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)

-   照片缩略图

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)

-   最大视频帧速率

    掌控：[**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_MAXVIDFPS\_PHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)

-   Flash 模式 (支持 KSCAMERA\_EXTENDEDPROP\_闪存\_SINGLEFLASH 功能)

    掌控：[**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)

 

 




