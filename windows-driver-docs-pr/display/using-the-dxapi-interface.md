---
title: 使用 DxApi 接口
description: 使用 DxApi 接口
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，DxApi 接口
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，DxApi 接口
- 内核模式视频传输 WDK DirectDraw，DxApi 接口
- 视频传输内核模式 WDK DirectDraw，DxApi 接口
- DxApi 接口 WDK DirectDraw
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8d368b3a7c26fb63d1e3d6db3bc63bb285c2e99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824163"
---
# <a name="using-the-dxapi-interface"></a>使用 DxApi 接口


## <span id="ddk_using_the_dxapi_interface_gg"></span><span id="DDK_USING_THE_DXAPI_INTERFACE_GG"></span>


如 [使用 Kernel-Mode 视频传输](using-kernel-mode-video-transport.md)中所述，视频捕获驱动程序 (硬件解码器) 必须调用 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数来访问 DxApi 接口。 如 [VPE 和 Kernel-Mode 视频传输体系结构](vpe-and-kernel-mode-video-transport-architecture.md)中所述， [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) 在 Windows 2000 和更高版本的平台上实现了 DxApi 接口。 以下部分介绍了如何在这些平台上支持 DxApi 接口：

[Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)

 

