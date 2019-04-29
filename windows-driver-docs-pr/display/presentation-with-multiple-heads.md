---
title: 使用多个头进行呈现
description: 使用多个头进行呈现
ms.assetid: 60405ea7-91d5-4deb-9161-8890faa7e897
keywords:
- 多个头硬件 WDK DirectX 9.0，演示文稿
- 演示文稿 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37ca5e1535322dd7fbf81e500c4e1ced7ffc7b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352217"
---
# <a name="presentation-with-multiple-heads"></a>使用多个头进行呈现


## <span id="ddk_presentation_with_multiple_heads_gg"></span><span id="DDK_PRESENTATION_WITH_MULTIPLE_HEADS_GG"></span>


应用程序可以调用**存在**方法一次性呈现所有头的后台缓冲区的内容，或能够提供单个头后台缓冲区。 有关详细信息**存在**，请参阅最新的 DirectX SDK 文档。

反过来，运行时做出对驱动程序的独立顺序调用[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)或[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数。 由于每个头部的显示模式和刷新率可能不同，这些调用始终是独立 DDI 级别。

 

 





