---
title: 在全屏幕上启用 Alpha 通道后台缓冲区
description: 在全屏幕上启用 Alpha 通道后台缓冲区
ms.assetid: 9d922464-fb1b-459b-9363-61afff7c51e3
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，alpha 通道上的全屏后台缓冲区
- 翻转链 WDK DirectX 8.0
- 主翻转链 WDK DirectX 8.0
- 全屏幕翻转链 WDK DirectX 8.0
- alpha 通道 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9829939051617356f0c62cd2eda516c4808b7f9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525967"
---
# <a name="enabling-alpha-channels-on-full-screen-back-buffers"></a>在全屏幕上启用 Alpha 通道后台缓冲区


## <span id="ddk_enabling_alpha_channels_on_full_screen_back_buffers_gg"></span><span id="DDK_ENABLING_ALPHA_CHANNELS_ON_FULL_SCREEN_BACK_BUFFERS_GG"></span>


DirectDraw DDI 中，在主翻转链创建具有任何内部函数的像素格式。 因此，在此链中的图面显示模式的像素格式对其执行。 例如，在 32bpp 模式下创建一个主翻转链将采用 D3DFMT\_X8R8G8B8 格式。

对于许多的全屏应用程序创建此类链。 因为链的后台缓冲区有无 alpha 通道，D3DRS\_ALPHABLENDENABLE 呈现状态和效果不佳定义目标应用层协议的相关联的 blend 呈现状态。 DirectX 8.1 引入了一项新功能 Direct3D 运行时用来通知应用程序的请求使用 alpha 通道的像素格式的这些图面中创建应用层的全屏幕翻转链的驱动程序。

若要指示此功能的支持，该驱动程序必须设置 D3DCAPS3\_ALPHA\_全屏\_翻转\_或者\_丢弃位 (在中定义*d3d8caps.h*文件) 中**Caps3** D3DCAPS8 结构中的成员。 该驱动程序在响应中返回 D3DCAPS8 结构**GetDriverInfo2**查询中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

确定支持此功能后，该驱动程序可以接收[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)调用 DDSCAPS2\_ENABLEALPHACHANNEL (中定义*ddraw.h*文件) 中设置位**dwCaps2**的成员[ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)结构。 此位仅设置以创建主翻转链的一部分或独立的后台缓冲区上的图面。

如果该驱动程序检测到此位，该驱动程序确定图面采用不显示模式的格式，但在显示模式下的格式和 alpha。 例如，在 32bpp 模式下，此类面应授予 D3DFMT\_A8R8G8B8 格式。

在 Windows XP 和更高版本上和在 Windows 2000 操作系统版本中，将安装的 DirectX 8.1 运行时提供了此功能。

 

 





