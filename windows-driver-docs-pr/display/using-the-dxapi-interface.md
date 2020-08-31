---
title: 使用 DxApi 接口
description: 使用 DxApi 接口
ms.assetid: 9de96d20-6cfc-42e7-821b-8256e0dd9b38
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，DxApi 接口
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，DxApi 接口
- 内核模式视频传输 WDK DirectDraw，DxApi 接口
- 视频传输内核模式 WDK DirectDraw，DxApi 接口
- DxApi 接口 WDK DirectDraw
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d9e7aa58e9e238f6219a942ad377652470e2dd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067090"
---
# <a name="using-the-dxapi-interface"></a>使用 DxApi 接口


## <span id="ddk_using_the_dxapi_interface_gg"></span><span id="DDK_USING_THE_DXAPI_INTERFACE_GG"></span>


如 [使用内核模式视频传输](using-kernel-mode-video-transport.md)中所述， (硬件解码器的视频捕获驱动程序) 必须调用 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数来访问 DxApi 接口。 如 [VPE 和内核模式视频传输体系结构](vpe-and-kernel-mode-video-transport-architecture.md)中所述， [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) 在 Windows 2000 和更高版本的平台上实现了 DxApi 接口。 以下部分介绍了如何在这些平台上支持 DxApi 接口：

[Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)

 

