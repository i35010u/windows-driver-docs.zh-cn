---
title: 私有 Display-Miniport 驱动程序 IOCTL_VIDEO_XXX 请求
description: 小型端口驱动程序可以为其相应的显示驱动程序定义一个或多个专用 i/o 控制代码。
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- 私下定义的 IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- I/o WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 219818616da652114e2971603234a5f859ae6d03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840755"
---
# <a name="privately-defined-display-miniport-driver-ioctl_video_xxx-requests"></a>私下定义 Display-Miniport 驱动程序 IOCTL \_ 视频 \_ XXX 请求

小型端口驱动程序可以为其相应的显示驱动程序定义一个或多个专用 i/o 控制代码。

但是，只有特定的显示和小型端口驱动程序对可以使用私下定义的 i/o 控制代码。 也就是说，设计为在现有显示器驱动程序下运行的微型端口驱动程序不应定义专用 i/o 控制代码，因为现有的显示驱动程序无法在不重写的情况下进行新的 i/o 控制请求，且可能不会损坏现有的已使用的微型端口驱动程序。 在许多不同型号的适配器（如 SVGA 适配器）上分层的现有或通用的显示驱动程序也不能依赖于私下定义的 i/o 控制代码，使每个基础微型端口驱动程序具有相同的效果。

有关定义专用 i/o 控制代码的详细信息，请参阅 [使用 I/o 控制代码](../kernel/introduction-to-i-o-control-codes.md)。

 

