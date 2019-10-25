---
title: VMR 视频处理
description: VMR 视频处理
ms.assetid: 149f881d-1a6e-46b7-9a37-971c7bb7b79d
keywords:
- ProcAmp WDK DirectX VA，VMR
- VMR WDK DirectX VA
- 渐进式视频 WDK DirectX VA
- mixers WDK VRM
- 颜色空间转换 WDK DirectX VA
- 管道 WDK VRM
- 水平调整 WDK VRM
- 硬件 WDK VRM
- 水平调整视频图像大小
- 转换颜色空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d0fae028b028ea79b47155606a59febff7b5ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825274"
---
# <a name="vmr-video-processing"></a>VMR 视频处理


## <span id="ddk_vmr_video_processing_gg"></span><span id="DDK_VMR_VIDEO_PROCESSING_GG"></span>


VMR 可以在显示视频之前对视频执行以下一系列处理操作。 VMR 的混合器组件始终按列出的顺序执行这些操作。 颜色空间转换和纵横比更正适用于所有视频流;其他操作是可选的。 VMR 仅执行视频播放应用程序所请求的操作。

-   ProcAmp 控件调整

-   取消隔行扫描

-   纵横比更正

-   颜色空间转换

-   垂直或水平镜像和 alpha 混合

只要有可能，VMR 的混合器就会将尽可能多的进程组合在一起，以减少处理视频所需的总体内存带宽。 这些进程的组合程度取决于硬件的功能。

本部分中的图例显示了 VMR 的混合器在 ProcAmp 控制操作期间处理视频的视频处理管道。 混音器执行的操作取决于硬件功能。 在插图中，矩形表示 Direct3D surface 和圆圈表示 Direct3D 或 DirectX VA 操作。 下图显示了以下功能的视频处理管道：

-   可以执行颜色空间转换和水平调整视频图像大小的硬件。

-   不能执行颜色空间转换且无法水平调整视频图像大小但可支持 YUV 纹理的硬件。

-   不能执行颜色空间转换的硬件，无法水平调整视频图像的大小，也不能支持 YUV 纹理。

VMR 的处理管道的输出图面总是 Direct3D 呈现器目标。 应用程序能够对 VMR 进行配置，以便输出呈现器目标也可以是 Direct3D 纹理或 Direct3D 交换链的一部分。

下图显示了当 ProcAmp 控制硬件能够执行颜色空间转换并水平调整视频图像大小时，VMR 用于处理*渐进式*视频的视频处理管道。

![阐释可执行颜色空间转换并水平调整视频图像大小的硬件的关系图](images/procamp1.png)

通常，视频播放应用程序不会请求 VMR 在显示时执行 alpha 混合或视频的垂直/水平镜像。 然后，VMR 可以将所有视频处理合并到一个阶段。 在这种情况下，将使用第一个管道。 如果应用程序请求 VMR 在显示前对视频图像执行 alpha 混合或垂直/水平镜像，则 VMR 会将额外的阶段插入管道。 在这种情况下，将使用第二个管道。

下图显示了当 ProcAmp 控制硬件无法执行颜色空间转换，并且在 ProcAmp 调整期间无法水平调整视频图像大小时，VMR 用于处理*渐进式*视频的视频管道操作（如 DXVA\_VideoProcess\_YUV2RGB 和 DXVA\_VideoProcess\_StretchX 枚举器[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_videoprocesscaps)中所示），但支持 YUV 纹理。

![说明无法执行颜色空间转换且无法水平调整大小但可支持 yuv 纹理的硬件的关系图](images/procamp2.png)

下图显示了当 ProcAmp 控制硬件无法执行颜色空间转换时 VMR 用于处理*渐进式*视频的视频管道，不能在 ProcAmp 调整操作期间水平调整视频图像大小（如 DXVA\_VideoProcess\_YUV2RGB 和 DXVA\_VideoProcess\_StretchX 枚举器[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_videoprocesscaps)中所示），并且不支持 YUV 纹理。

![说明无法执行颜色空间转换、无法水平调整大小以及不支持 yuv 纹理的关系图](images/procamp3.png)

如果应用程序未请求对视频图像进行任何 alpha 混合或镜像，则 VMR 会使用第一个管道。 如果应用程序请求 alpha 混合或视频图像的镜像，则 VMR 会使用第二个管道。

 

 





