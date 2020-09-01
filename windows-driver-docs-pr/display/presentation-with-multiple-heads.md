---
title: 使用多个头进行呈现
description: 使用多个头进行呈现
ms.assetid: 60405ea7-91d5-4deb-9161-8890faa7e897
keywords:
- 多头硬件 WDK DirectX 9.0，演示
- 演示文稿 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2eebeb85a276accf47d241749d3cf9ee113a4ea
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066454"
---
# <a name="presentation-with-multiple-heads"></a>使用多个头进行呈现


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


应用程序可以调用 **当前** 的方法，以便一次为所有 head 显示后台缓冲区的内容，或者显示单个头的后台缓冲区。 有关 **现有**的详细信息，请参阅最新的 DirectX SDK 文档。

运行时反过来使对驱动程序的 [*DdFlip*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 或 [*DdBlt*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数进行独立的顺序调用。 由于每个 head 的显示模式和刷新速率可能不同，因此这些调用在 DDI 级别上始终是独立的。

 

