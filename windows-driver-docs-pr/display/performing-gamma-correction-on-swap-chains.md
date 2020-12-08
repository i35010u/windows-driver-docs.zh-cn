---
title: 针对交换链执行灰度校正
description: 针对交换链执行灰度校正
keywords:
- 伽玛更正 WDK DirectX 9.0，交换链
- 交换链 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3f082951ec6ffc5c60d8806cd6d9aea1aba47bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838063"
---
# <a name="performing-gamma-correction-on-swap-chains"></a>针对交换链执行灰度校正


## <span id="ddk_performing_gamma_correction_on_swap_chains_gg"></span><span id="DDK_PERFORMING_GAMMA_CORRECTION_ON_SWAP_CHAINS_GG"></span>


应用程序可以在线性颜色空间内维护其交换链的后台缓冲区，以便正确执行混合操作。 由于桌面通常不在线性颜色空间中，因此需要对后台缓冲区内容进行伽玛更正，然后才能在桌面上显示内容。

应用程序调用 **IDirect3DSwapChain9：:P 重发** 方法，以显示交换链中下一个后台缓冲区的内容。 在此调用中，若要指示后台缓冲区内容处于线性颜色空间中，应用程序会设置 D3DPRESENT \_ 线性 \_ 内容标志。 然后，DirectX 9.0 运行时将显示驱动程序的 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数与 DdBlt \_ 扩展 \_ 标志和 DdBlt \_ 扩展的 \_ 线性 \_ 内容标志集一起调用。 当驱动程序收到此 *DdBlt* 调用时，驱动程序将确定源图面在线性颜色空间中包含内容。 然后，该驱动程序可以在线性颜色空间上执行伽玛2.2 矫正 (sRGB) 作为 blt 的一部分。 有关扩展的 array.blit 标志的详细信息，请参阅 [扩展的 Blt 标志](extended-blt-flags.md)。

驱动程序在 \_ \_ \_ \_ D3DCAPS9 结构的 **Caps3** 成员中将 D3DCAPS3 线性设置为 SRGB 表示功能位，以指示其设备支持伽玛2.2 更正。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

有关 **IDirect3DSwapChain:P *Xxx*** 的详细信息，请参阅最新的 DirectX SDK 文档。

 

