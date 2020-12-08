---
title: Windows 2000 视频微型端口驱动程序的责任
description: Windows 2000 视频微型端口驱动程序的责任
keywords:
- 显示驱动程序模型 WDK Windows 2000，责任
- Windows 2000 显示器驱动程序模型 WDK，责任
- 视频微型端口驱动程序 WDK Windows 2000，责任
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28b1a6d7b67db6bd1745c3038120b2e9e42fc780
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825995"
---
# <a name="windows-2000-video-miniport-driver-responsibilities"></a>Windows 2000 视频微型端口驱动程序的责任


## <span id="ddk_video_miniport_driver_responsibilities_gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_RESPONSIBILITIES_GG"></span>


内核模式 *视频微型端口驱动程序* ( .sys 文件) 通常处理必须与其他 NT 内核组件进行交互的操作。 例如，诸如硬件初始化和内存映射等操作需要 NT i/o 子系统的操作。 视频微型端口驱动程序的责任包括资源管理，如硬件配置和物理设备内存映射。 视频微型端口驱动程序必须特定于视频硬件。

显示驱动程序对不常请求的操作使用视频微型端口驱动程序;例如，若要管理资源，请执行物理设备内存映射，确保注册输出出现在接近或响应中断的情况下。

**注意**   视频微型端口驱动程序必须管理所有资源， (例如，视频微型端口驱动程序与显示驱动程序之间共享) 内存资源。 系统不保证显示驱动程序中获取的资源始终可由视频微型端口驱动程序访问。

 

视频微型端口驱动程序还处理：

-   模式集与图形卡的交互。

-   多个硬件类型，最小化显示驱动程序中的硬件类型依赖关系。

-   将视频寄存器映射到显示驱动程序的地址空间。 I/o 端口可直接寻址。

[Windows 2000 显示器驱动程序模型中的视频微型端口驱动](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)程序中详细讨论了视频微型端口驱动程序。

 

 





