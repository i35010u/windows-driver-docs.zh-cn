---
title: 使用 DxApi 接口
description: 使用 DxApi 接口
ms.assetid: 9de96d20-6cfc-42e7-821b-8256e0dd9b38
keywords:
- 绘制内核模式视频传输 WDK DirectDraw DxApi 接口
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，DxApi 接口
- 内核模式视频传输 WDK DirectDraw，DxApi 接口
- 视频传输内核模式 WDK DirectDraw，DxApi 接口
- DxApi 接口 WDK DirectDraw
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c09ce1ea8d6fe9d780be335ed143b6e41030718
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388994"
---
# <a name="using-the-dxapi-interface"></a>使用 DxApi 接口


## <span id="ddk_using_the_dxapi_interface_gg"></span><span id="DDK_USING_THE_DXAPI_INTERFACE_GG"></span>


如中所述[使用内核模式视频传输](using-kernel-mode-video-transport.md)，视频捕获驱动程序 （硬件解码器） 必须调用[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)函数来访问 DxApi 接口。 如中所述[VPE 和内核模式视频传输体系结构](vpe-and-kernel-mode-video-transport-architecture.md)即[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)Windows 2000 和更高版本的平台上实现 DxApi 接口。 以下部分介绍如何在这些平台上支持 DxApi 接口：

[DxApi 微型端口驱动程序功能适用于 Windows 2000 及更高版本](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)

 

 





