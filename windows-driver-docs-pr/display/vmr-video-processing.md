---
title: VMR 视频处理
description: VMR 视频处理
ms.assetid: 149f881d-1a6e-46b7-9a37-971c7bb7b79d
keywords:
- ProcAmp WDK DirectX VA , VMR
- VMR WDK DirectX VA
- 渐进式视频 WDK DirectX VA
- 搅拌机 WDK VRM
- 颜色空间转换 WDK DirectX VA
- 管道 WDK VRM
- 水平调整大小 WDK VRM
- hardware WDK VRM
- 水平调整视频图像的大小
- 将颜色空间转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06ebeef1b0248d627d16c43ef2df6161eb0496de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381847"
---
# <a name="vmr-video-processing"></a>VMR 视频处理


## <span id="ddk_vmr_video_processing_gg"></span><span id="DDK_VMR_VIDEO_PROCESSING_GG"></span>


VMR 可以执行以下一系列显示前处理的视频的操作。 VMR 混音器组件始终按所列顺序执行这些操作。 颜色空间转换和纵横比更正应用于所有视频流;其他操作是可选的。 VMR 执行请求的视频播放应用程序的那些操作。

-   ProcAmp 控制调整

-   去隔行

-   长宽比校正

-   颜色空间转换

-   垂直或水平镜像和 alpha 值混合处理

只要有可能，VMR 混音器组合任意数量的这些流程作为可减少处理视频所需的整体内存带宽。 这些进程可以合并到的程度取决的硬件功能。

本部分中的图例显示处理管道 VMR 混音器处理视频 ProcAmp 控制操作期间使用的视频。 混音器执行的操作取决于硬件的功能。 在插图中，矩形表示 Direct3D 图面和圆圈表示 Direct3D 或 DirectX VA 操作。 在图所示的以下功能的视频处理管道：

-   可以执行颜色空间转换和水平调整视频图像的大小的硬件。

-   不能执行颜色空间转换和不能水平调整视频的图像，但可以支持 YUV 纹理的硬件。

-   无法执行颜色空间转换的硬件不能水平调整视频的图像，而且无法支持 YUV 纹理。

VMR 的处理管道的输出接口始终是 Direct3D 呈现器目标。 应用程序才能够配置 VMR 以便 Direct3D 纹理或 Direct3D 交换链的一部分，也可能是输出呈现器目标。

下图显示了 VMR 用来处理视频处理管道*渐进式*视频 ProcAmp 控制硬件时能够执行颜色空间转换和水平调整视频图像的大小。

![说明硬件，可以执行颜色空间转换并调整视频图像的水平大小的关系图](images/procamp1.png)

通常情况下，视频播放应用程序不会请求 VMR 执行 alpha 值混合处理或垂直/水平镜像视频作为它的显示。 VMR 便能将合并到单个阶段处理的所有视频。 在这种情况下，使用第一个管道。 如果应用程序请求 VMR 执行 alpha 值混合处理或垂直/水平镜像的视频图像之前显示，VMR 将插入到管道的附加阶段。 在这种情况下，使用第二个管道。

下图显示了 VMR 用来处理视频管道*渐进式*视频时 ProcAmp 控制硬件不能执行颜色空间转换和不能水平调整期间视频图像的大小ProcAmp 调整操作 (由 DXVA\_VideoProcess\_YUV2RGB 和 DXVA\_VideoProcess\_StretchX 中的枚举器[ **DXVA\_VideoProcessCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_videoprocesscaps))，但支持 YUV 纹理。

![说明不能执行颜色空间转换和不能调整水平大小，但可以支持 yuv 纹理的硬件的关系图](images/procamp2.png)

下图显示了 VMR 用来处理视频管道*渐进式*视频时 ProcAmp 控制硬件不能执行颜色空间转换，不能在 ProcAmp 期间水平调整视频图像调整操作 (由 DXVA\_VideoProcess\_YUV2RGB 和 DXVA\_VideoProcess\_StretchX 中的枚举器[ **DXVA\_VideoProcessCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_videoprocesscaps))，并且不支持 YUV 纹理。

![说明不能执行颜色空间转换、 水平，不能调整大小和不能支持 yuv 纹理硬件的关系图](images/procamp3.png)

如果应用程序未请求任何 alpha 值混合处理或镜像的视频图像，VMR 使用第一个管道。 如果应用程序请求任一 alpha 值混合处理或镜像的视频图像将 VMR 使用第二个管道。

 

 





