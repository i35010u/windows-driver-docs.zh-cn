---
title: 在 IAMVideoAccelerator API DXVA 和运动补偿 DDI
description: DirectX VA 与 IAMVideoAccelerator API 和运动补偿 DDI 之间的关系
ms.assetid: 8bfa198f-b29f-491f-8133-a1f3b41e0cbe
keywords:
- DirectX 视频加速 WDK Windows 2000 显示 IAMVideoAccelerator
- 视频加速 WDK DirectX IAMVideoAccelerator
- VA WDK DirectX IAMVideoAccelerator
- IAMVideoAcceleratorNotify
- IAMVideoAccelerator
- 视频混合呈现器 WDK DirectX VA
- VMR WDK DirectX VA
- 覆盖 mixer WDK DirectX VA
- OVM WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 788b25ccf393d830c439dece55781c819c07f53e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565462"
---
# <a name="directx-va-relationship-to-iamvideoaccelerator-api-and-motion-compensation-ddi"></a>DirectX VA 与 IAMVideoAccelerator API 和运动补偿 DDI 之间的关系

使用 DirectX VA **IAMVideoAcceleratorNotify**和**IAMVideoAccelerator**接口 （记录在 Microsoft Windows SDK） 中，并且[动作补偿 DDI](motion-compensation.md)若要指定的软件解码器之间交换的数据格式，呈现器 (VMR) 或覆盖 mixer (OVM) 混合视频和视频显示器驱动程序。 下图显示软件解码器、 VMR，和视频显示器驱动程序，这些接口的关系。

![说明 directx va 数据流关系图](images/iamvideo.png)

**IAMVideoAcceleratorNotify**接口检索或设置给定视频 accelerator GUID 的解压缩的缓冲区信息。

**IAMVideoAccelerator**接口使视频解码器筛选器可访问视频加速器的功能，并提供使用混合使用呈现器 (VMR) 或覆盖 mixer (OVM) 的视频的视频呈现。

运动补偿 DDI 建立公共接口，以访问硬件加速功能，并支持跨供应商用户模式下的软件应用程序和加速功能之间的兼容性。 DDI 通知解码器视频加速对象正在使用、 启动和停止的帧缓冲区解码时指示的未压缩的图片格式的硬件支持，并通知需要使显示驱动程序呈现。 通过访问 DDI 的运动补偿[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)结构。

有关详细信息**IAMVideoAccelerator**并**IAMVideoAcceleratorNotify**接口，请参阅 Windows SDK 文档。 有关运动补偿 DDI 的详细信息，请参阅[运动补偿](motion-compensation.md)并[运动补偿回调](motion-compensation-callbacks.md)。

 

 





