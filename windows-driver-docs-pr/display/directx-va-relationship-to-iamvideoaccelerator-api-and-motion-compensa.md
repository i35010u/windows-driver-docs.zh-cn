---
title: IAMVideoAccelerator API 中的 DXVA 和运动补偿 DDI
description: DirectX VA 与 IAMVideoAccelerator API 和运动补偿 DDI 之间的关系
ms.assetid: 8bfa198f-b29f-491f-8133-a1f3b41e0cbe
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，IAMVideoAccelerator
- 视频加速 WDK DirectX，IAMVideoAccelerator
- VA WDK DirectX，IAMVideoAccelerator
- IAMVideoAcceleratorNotify
- IAMVideoAccelerator
- 视频混合呈现器 WDK DirectX VA
- VMR WDK DirectX VA
- 覆盖混音器 WDK DirectX VA
- OVM WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 8444f61f47f36ee129e4f2f50611195978347647
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067448"
---
# <a name="directx-va-relationship-to-iamvideoaccelerator-api-and-motion-compensation-ddi"></a>DirectX VA 与 IAMVideoAccelerator API 和运动补偿 DDI 之间的关系

DirectX VA 使用 Microsoft Windows SDK) 中所述的 **IAMVideoAcceleratorNotify** 和 **IAMVideoAccelerator** 接口 (， [以及用于指定](motion-compensation.md) 软件解码器、视频混合呈现器 (VMR) 或覆盖混音器 (OVM) 和视频显示器驱动程序之间交换的数据格式的数据的格式。 下图显示了这些接口与软件解码器、VMR 和视频显示器驱动程序之间的关系。

![阐释 directx va 数据流的图示](images/iamvideo.png)

**IAMVideoAcceleratorNotify**接口检索或设置给定视频加速器 GUID 的解压缩缓冲区信息。

**IAMVideoAccelerator**接口允许视频解码器筛选器访问视频加速器的功能，并使用视频混合呈现器 (VMR) 或覆盖混音器 (OVM) 提供视频呈现。

运动补偿 DDI 建立了一个公共接口，用于访问硬件加速功能，并允许在用户模式软件应用程序和加速功能之间实现跨供应商的兼容性。 当使用视频加速对象时，DDI 会通知解码器，启动和停止帧缓冲区解码，指示硬件支持的未压缩图片格式，并通知需要呈现的 macroblocks 的显示驱动程序。 运动补偿 DDI 通过 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) 结构访问。

有关 **IAMVideoAccelerator** 和 **IAMVideoAcceleratorNotify** 接口的详细信息，请参阅 Windows SDK 文档。 有关运动补偿 DDI 的详细信息，请参阅 [运动补偿](motion-compensation.md) 和 [运动补偿回拨](motion-compensation-callbacks.md)。

 

