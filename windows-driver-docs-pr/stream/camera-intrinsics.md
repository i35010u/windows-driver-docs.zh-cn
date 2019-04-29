---
title: 相机内部函数
description: 提供有关照相机内部函数的信息。
ms.date: 09/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06081bc39204298abdf8899239d31d9fa1e6de9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370497"
---
# <a name="camera-intrinsics"></a>相机内部函数

照相机驱动程序 （或或者，通过 DMFT） 可以将照相机内部函数属性附加到流属性存储 using [MFStreamExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfstreamextension-pinholecameraintrinsics)，或将附加到媒体帧属性存储 using [MFSampleExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfsampleextension-pinholecameraintrinsics)。 如果它已附加到的流属性存储，照相机内部函数的值将不会更改在相机的流处理过程。 如果它已附加到媒体帧属性存储，则内部函数值可能会更改每个帧。 

对于上述两个属性，该值必须是类型的结构[MFPinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfpinholecameraintrinsics)，报告照相机内部模型的列表。 此列表中的每个条目是与类型[MFPinholeCameraIntrinsic_IntrinsicModel](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-mfpinholecameraintrinsic_intrinsicmodel)，包含解析 （宽度/高度）、 pinhole 模型，并[MFCameraIntrinsic_DistortionModel](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfcameraintrinsic_distortionmodel)扭曲模型. 

使用时**MFPinholeCameraIntrinsics**流属性存储区中，使用此列表必须包含至少一个，并可能很多内部函数的模型。 系统将选择基于通过匹配的宽度和高度的帧的正在流式处理的帧格式的内部函数模型。 如果找到完全匹配，则将使用内部函数。 否则，使用相同的纵横比的第一个内部函数将改为使用，例如，如果列表包含两个条目，640 x 480 和 1920 x 1080，分别。 如果流式处理与 1280 x 720 媒体格式，将使用适当的缩放使用 1080p 内部函数。 

使用时**MFPinholeCameraIntrinsics**媒体帧属性存储区中，使用此列表必须包含具有相同的帧分辨率的分辨率且只有一个内部函数模型。
