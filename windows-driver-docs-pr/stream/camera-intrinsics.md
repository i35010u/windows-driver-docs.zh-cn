---
title: 相机内部函数
description: 提供有关照相机内部函数的信息。
ms.date: 09/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4d2e6a0f102f02e638bdabd5961e99c06be82da8
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802531"
---
# <a name="camera-intrinsics"></a>相机内部函数

照相机驱动程序 (或通过 DMFT) 可以使用 [MFStreamExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfstreamextension-pinholecameraintrinsics)将照相机内部函数属性附加到流属性存储，或使用 [MFSampleExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfsampleextension-pinholecameraintrinsics)附加到媒体帧属性存储。 如果已将其附加到流属性存储，则在相机流式处理期间，照相机内部函数的值不会更改。 如果已将其附加到媒体帧属性存储，则每个帧的内部函数值可能会更改。 

对于上述两个属性，该值必须是 [MFPinholeCameraIntrinsics](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-_mfpinholecameraintrinsics)类型的结构，该结构报告照相机内部模型的列表。 此列表中的每个条目都包含类型 [MFPinholeCameraIntrinsic_IntrinsicModel](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-mfpinholecameraintrinsic_intrinsicmodel)，其中包含 (宽度/高度) 、pinhole 模型和 [MFCameraIntrinsic_DistortionModel](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-_mfcameraintrinsic_distortionmodel) 扭曲模型的分辨率。 

将 **MFPinholeCameraIntrinsics** 与 stream 属性存储一起使用时，此列表必须包含至少一个内部模型，可能包含很多内部模型。 系统将通过匹配帧的宽度和高度来选择基于主动流式处理帧格式的内部函数。 如果找到完全匹配项，将使用内部函数。 否则，将改为使用具有相同纵横比的第一个内部函数，例如，当列表中分别包含两个条目时，则会使用640x480 和1920x1080。 如果使用1280x720 媒体格式进行流式处理，则1080p 内部函数将用于适当的缩放。 

将 **MFPinholeCameraIntrinsics** 与媒体帧属性存储一起使用时，此列表必须只包含一个内部函数，其分辨率与帧分辨率相同。
