---
title: 使用多个头进行呈现
description: 使用多个头进行呈现
keywords:
- 多头硬件 WDK DirectX 9.0，演示
- 演示文稿 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a24137bf07e7909d9ed878e0badb4e22e1101f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833049"
---
# <a name="presentation-with-multiple-heads"></a>使用多个头进行呈现


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


应用程序可以调用 **当前** 的方法，以便一次为所有 head 显示后台缓冲区的内容，或者显示单个头的后台缓冲区。 有关 **现有** 的详细信息，请参阅最新的 DirectX SDK 文档。

运行时反过来使对驱动程序的 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 或 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数进行独立的顺序调用。 由于每个 head 的显示模式和刷新速率可能不同，因此这些调用在 DDI 级别上始终是独立的。

 

