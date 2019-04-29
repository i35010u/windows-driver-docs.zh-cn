---
title: 针对交换链执行灰度校正
description: 针对交换链执行灰度校正
ms.assetid: 4912cd15-bd56-43b6-9419-66917bf3f72c
keywords:
- 灰度校正 WDK DirectX 9.0 中，交换链
- 交换链 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c13863c106121237614da6f9ded40f4302a26655
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352253"
---
# <a name="performing-gamma-correction-on-swap-chains"></a>针对交换链执行灰度校正


## <span id="ddk_performing_gamma_correction_on_swap_chains_gg"></span><span id="DDK_PERFORMING_GAMMA_CORRECTION_ON_SWAP_CHAINS_GG"></span>


若要正确执行混合操作，应用程序可以维护线性颜色空间中其交换链后台的缓冲区。 因为桌面通常不是线性的颜色空间中，后台缓冲区的内容的灰度校正是必需的之前可以在桌面上显示内容。

应用程序调用**IDirect3DSwapChain9::Present**方法来交换链中存在的下一步的后台缓冲区的内容。 在此调用，用于指示后缓冲区内容是线性颜色空间中，应用程序设置 D3DPRESENT\_线性\_内容的标志。 DirectX 9.0 运行时，都依次调用显示器驱动程序[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数和 DDBLT\_扩展\_标志和 DDBLT\_扩展\_线性\_内容标记集。 当驱动程序收到这*DdBlt*调用时，该驱动程序确定源面包含线性颜色空间中的内容。 驱动程序可以继续执行上一部分 blt 线性颜色空间 gamma 2.2 更正 (sRGB)。 有关扩展的 blit 标志的详细信息，请参阅[扩展 Blt 标志](extended-blt-flags.md)。

驱动程序设置 D3DCAPS3\_线性\_TO\_SRGB\_呈现功能中的位**Caps3** D3DCAPS9 结构的成员，以指示其设备支持 gamma 2.2更正。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

有关详细信息**IDirect3DSwapChain*Xxx*:: 存在**，请参阅最新的 DirectX SDK 文档。

 

 





