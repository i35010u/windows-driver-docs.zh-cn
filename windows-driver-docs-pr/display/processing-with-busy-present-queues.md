---
title: 处理繁忙呈现队列
description: 处理繁忙呈现队列
ms.assetid: 5fce137b-001c-49f6-85ad-94c9eead9aa0
keywords:
- 繁忙存在队列 WDK DirectX 9.0
- 存在队列 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ca64f2ad43c100ce617a6239331540319d4656
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370167"
---
# <a name="processing-with-busy-present-queues"></a>处理繁忙呈现队列


## <span id="ddk_processing_with_busy_present_queues_gg"></span><span id="DDK_PROCESSING_WITH_BUSY_PRESENT_QUEUES_GG"></span>


DirectX 9.0 版本驱动程序必须返回 DDERR\_WASSTILLDRAWING 值通过调用其[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)函数如果在运行时传递 DDFLIP\_中的 DONOTWAIT 标志**dwFlags**的成员[ **DD\_FLIPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551520)结构和驱动程序不能计划的演示内容，例如，如果存在队列是 full 或驱动程序是否正在等待的垂直同步间隔。 运行时调用的驱动程序*DdFlip*函数与 DDFLIP\_DONOTWAIT 设置，如果应用程序调用**IDirect3DSwapChain9::Present** D3DPRESENT 方法\_设置 DONOTWAIT 标志。 如果该驱动程序不能安排一个演示文稿，其*DdFlip*函数将返回 DDERR\_中的 WASSTILLDRAWING **ddRVal**的 DD 成员\_FLIPDATA。 应用程序的**存在**方法又会返回 DDERR\_WASSTILLDRAWING，这使应用程序执行其他处理。

D3DPRESENT\_DONOTWAIT 标志是 DirectX 9.0 的新增功能。 DDFLIP\_DONOTWAIT 标志问世以来 DirectX 7.0。 DirectX 7.0 应用程序时设置 DDFLIP\_对的调用中 DONOTWAIT **IDirectDrawSurface7::Flip**方法、 DirectX 7.0 或更高版本的驱动程序*DdFlip*函数会收到 DDFLIP\_DONOTWAIT 标志。

如果 D3DPRESENT\_DONOTWAIT 未设置，**存在**如下所示 DirectX 8.1 及更早版本的行为。 即**存在**旋转，直到硬件是免费的而不返回错误。

有关详细信息**IDirect3DSwapChain*Xxx*:: 存在**，请参阅最新的 DirectX SDK 文档。

 

 





