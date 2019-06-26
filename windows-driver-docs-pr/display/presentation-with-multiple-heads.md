---
title: 使用多个头进行呈现
description: 使用多个头进行呈现
ms.assetid: 60405ea7-91d5-4deb-9161-8890faa7e897
keywords:
- 多个头硬件 WDK DirectX 9.0，演示文稿
- 演示文稿 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1de73f1b6d7360ff3f48dc7a1dde9af6b2a6fdfc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363740"
---
# <a name="presentation-with-multiple-heads"></a>使用多个头进行呈现


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


应用程序可以调用**存在**方法一次性呈现所有头的后台缓冲区的内容，或能够提供单个头后台缓冲区。 有关详细信息**存在**，请参阅最新的 DirectX SDK 文档。

反过来，运行时做出对驱动程序的独立顺序调用[ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)或[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数。 由于每个头部的显示模式和刷新率可能不同，这些调用始终是独立 DDI 级别。

 

 





