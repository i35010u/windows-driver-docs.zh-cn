---
title: Windows 2000 视频微型端口驱动程序责任
description: Windows 2000 视频微型端口驱动程序责任
ms.assetid: 55301260-af1b-4ef7-8f33-e0acbeb22039
keywords:
- 显示器驱动程序模型 WDK Windows 2000，职责
- Windows 2000 显示器驱动程序模型 WDK，职责
- 微型端口驱动程序 WDK Windows 2000，职责
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bd067752ea118b5e99968f6e52819f99ac66e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543970"
---
# <a name="windows-2000-video-miniport-driver-responsibilities"></a>Windows 2000 视频微型端口驱动程序责任


## <span id="ddk_video_miniport_driver_responsibilities_gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_RESPONSIBILITIES_GG"></span>


内核模式*微型端口驱动程序*（.sys 文件） 通常处理必须与其他 NT 内核组件进行交互的操作。 例如，如硬件初始化和内存映射操作由 NT I/O 子系统需要操作。 微型端口驱动程序责任包括资源管理，例如，硬件配置和物理设备内存映射。 微型端口驱动程序必须是特定于视频硬件。

显示驱动程序使用不频繁请求; 的操作的微型端口驱动程序例如，若要管理资源，执行物理设备内存映射，请确保输出响应的中断或发生邻近，该寄存器。

**请注意**  微型端口驱动程序必须管理的微型端口驱动程序和显示驱动程序之间共享的所有资源 （例如，内存资源）。 系统不保证始终将微型端口驱动程序可以访问在显示器驱动程序中获取的资源。

 

微型端口驱动程序还可以处理：

-   设置与图形卡的交互模式。

-   多个硬件类型，最小化显示驱动程序中的硬件类型依赖项。

-   映射到显示器驱动程序的地址空间的视频寄存器。 I/O 端口是可直接寻址。

中详细讨论微型端口驱动程序[视频的微型端口驱动程序在 Windows 2000 显示器驱动程序模型](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)。

 

 





