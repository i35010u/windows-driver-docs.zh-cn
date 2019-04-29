---
title: DirectX 视频加速
description: DirectX 视频加速
ms.assetid: e25407a3-be5c-4509-a3e7-d9688958e3d4
keywords:
- DirectX 视频加速 WDK Windows 2000 显示
- 视频加速 WDK DirectX
- 运动补偿 WDK
- VA WDK DirectX
- 加速器 WDK DirectX
- 显示驱动程序模型 WDK Windows 2000 中，DirectX 视频加速
- Windows 2000 显示器驱动程序模型 WDK，DirectX 视频加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bfd057e9da495f3b0a67b0d9cd18e226052a8ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386996"
---
# <a name="directx-video-acceleration"></a>DirectX 视频加速


## <span id="ddk_directx_video_acceleration_gg"></span><span id="DDK_DIRECTX_VIDEO_ACCELERATION_GG"></span>


本部分包含有关 Microsoft DirectX 视频加速 (DirectX VA) 的信息。 这是一个应用程序编程接口 (API) 和相应[动作补偿](motion-compensation.md)设备驱动程序接口 (DDI) 加速数字视频解码。 此外提供以下其他 DDIs DirectX VA 的一部分：

-   一个[去隔行 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552701)去隔行和帧速率转换视频内容。

-   一个[ProcAmp DDI](https://msdn.microsoft.com/library/windows/hardware/ff569186)以支持 ProcAmp 控件和后续处理的视频内容。

-   一个[COPP DDI](sample-functions-for-copp.md)保护视频内容。

对于要创建 DirectX VA 驱动程序对于应使用 Microsoft Windows XP Service Pack 1 (SP1) 和更高版本的驱动程序编写人员*dxva.h*标头文件。 这包含的结构和枚举用于视频加速和去隔行和帧速率转换。

本部分包括以下主题：

[DirectX VA 简介](introduction-to-directx-va.md)

[视频解码](video-decoding.md)

[取消隔行和帧速率转换](deinterlacing-and-frame-rate-conversion.md)

[ProcAmp 控制处理](procamp-control-processing.md)

[COPP 处理](copp-processing.md)

[适用于 DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)

[DirectX VA 数据流管理](directx-va-data-flow-management.md)

[DirectX VA 操作](directx-va-operations.md)

[定义加速器功能](defining-accelerator-capabilities.md)