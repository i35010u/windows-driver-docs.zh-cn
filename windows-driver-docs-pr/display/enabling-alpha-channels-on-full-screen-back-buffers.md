---
title: 在全屏后端缓冲区中启用 Alpha 通道
description: 在全屏后端缓冲区中启用 Alpha 通道
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，全屏幕后台缓冲区上的 alpha 通道
- 翻转链 WDK DirectX 8。0
- 主翻转链 WDK DirectX 8。0
- 全屏翻转链 WDK DirectX 8。0
- alpha 通道 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc98857dde4e94ebd7e56d11ea08e5a07ef6ee06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816867"
---
# <a name="enabling-alpha-channels-on-full-screen-back-buffers"></a>在全屏后端缓冲区中启用 Alpha 通道


## <span id="ddk_enabling_alpha_channels_on_full_screen_back_buffers_gg"></span><span id="DDK_ENABLING_ALPHA_CHANNELS_ON_FULL_SCREEN_BACK_BUFFERS_GG"></span>


在 DirectDraw DDI 中，主翻转链的创建没有内部像素格式。 因此，此链中的表面采用显示模式的像素格式。 例如，在32bpp 模式下创建的主翻转链采用 D3DFMT \_ X8R8G8B8 格式。

此类链是为许多全屏应用程序创建的。 由于链的后台缓冲区没有 alpha 通道，因此 D3DRS \_ ALPHABLENDENABLE 呈现状态和目标图面的关联混合呈现状态定义不佳。 DirectX 8.1 引入了一项新功能，Direct3D 运行时使用此功能来通知应用程序请求的驱动程序，以在这些图面的像素格式中创建带有 alpha 通道的图面的全屏翻转链。

若要指明此功能的支持，驱动程序必须将 D3DCAPS3 \_ ALPHA \_ 全屏 \_ 翻转 \_ 或 \_ 放弃在 D3DCAPS8 结构的 **Caps3** 成员) 中定义的位 (。 *d3d8caps.h* 驱动程序将返回 D3DCAPS8 结构来响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

确定对此功能的支持之后，驱动程序可以接收 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))调用，其中 DDSCAPS2 \_ ENABLEALPHACHANNEL (在 [**dwCaps2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的 **DDSCAPS2** 成员中设置的 *ddraw*) 文件中定义。 此位仅被设置为创建属于主翻转链或独立后台缓冲区的图面。

如果驱动程序检测到这种情况，则驱动程序将确定表面不是显示模式的格式，而是显示模式的格式加 alpha。 例如，在32bpp 模式下，应为此类面提供 D3DFMT \_ A8R8G8B8 格式。

此功能在 Windows XP 及更高版本以及安装了 DirectX 8.1 运行时的 Windows 2000 操作系统版本上可用。

 

