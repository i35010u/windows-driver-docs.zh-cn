---
title: 处理繁忙呈现队列
description: 处理繁忙呈现队列
keywords:
- 忙显示队列 WDK DirectX 9。0
- 显示队列 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94945b5cdf4e633e4469cd19c6a3c83b78a37b1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840997"
---
# <a name="processing-with-busy-present-queues"></a>处理繁忙呈现队列


## <span id="ddk_processing_with_busy_present_queues_gg"></span><span id="DDK_PROCESSING_WITH_BUSY_PRESENT_QUEUES_GG"></span>


\_如果运行时在 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) \_ [**DD \_ DONOTWAIT**](/windows/win32/api/ddrawint/ns-ddrawint-dd_flipdata)结构的 **dwFlags** 成员中传递了 DdFlip FLIPDATA 标志，并且驱动程序无法计划显示（例如，如果当前队列已满或驱动程序正在等待 vsync 间隔），则 DirectX 9.0 版本驱动程序必须从对其 DdFlip 函数的调用返回 DDERR WASSTILLDRAWING 值。 *DdFlip* \_ 如果应用程序调用 **:P** 了 D3DPRESENT DONOTWAIT 标志，则运行时将使用 DdFlip DONOTWAIT Set 调用驱动程序的 DdFlip 函数 \_ 。 如果驱动程序无法计划演示，则其 *DdFlip* 函数 \_ 将在 DD FLIPDATA 的 **DDRVAL** 成员中返回 DDERR WASSTILLDRAWING \_ 。 应用程序的 **当前** 方法又返回 DDERR \_ WASSTILLDRAWING，这使应用程序可以执行其他处理。

D3DPRESENT \_ DONOTWAIT 标志是 DirectX 9.0 的新增标志。 \_从 DirectX 7.0 开始，DDFLIP DONOTWAIT 标志已可用。 如果 DirectX 7.0 应用程序要 \_ 在对 **IDirectDrawSurface7：： Flip** 方法的调用中设置 DDFLIP DONOTWAIT，则 directx 7.0 或更高版本的驱动程序的 *DDFLIP* 函数会收到 DDFLIP \_ DONOTWAIT 标志。

如果 \_ 未设置 D3DPRESENT DONOTWAIT，则 **提供** 的行为方式与 DirectX 8.1 和更早版本相同。 也就是说，一直 **旋转直到硬件可用，而** 不返回错误。

有关 **IDirect3DSwapChain:P *Xxx*** 的详细信息，请参阅最新的 DirectX SDK 文档。

 

