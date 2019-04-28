---
title: 同步两个或多个流
description: 同步两个或多个流
ms.assetid: c25f4ca2-8a9f-43bc-a1bf-b71826b446ff
keywords:
- HD Audio，同步流
- 高清晰度音频 (HD Audio)，同步流
- 同步流 WDK 音频
- 同步 WDK 音频进行流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6337fdd010ab9717d0c11e3edf1786569632cb1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328561"
---
# <a name="synchronizing-two-or-more-streams"></a>同步两个或多个流


[ **SetDmaEngineState** ](https://msdn.microsoft.com/library/windows/hardware/ff537889)例程的一个或多个 DMA 引擎将状态设置为以下值之一： 运行、 暂停、 停止或重置。 如果对此例程的调用指定一个以上的 DMA 引擎，然后所有 DMA 引擎进行状态转换以同步方式。

对于某些音频的应用程序需要同步组流的能力。 例如，音频驱动程序可能使用编解码器组合来创建逻辑环绕声音频设备，它将联接两个音频编解码器： 一个编解码器驱动器前扬声器和第二个音频编解码器驱动器后演讲者。 具体取决于编解码器的功能，音频驱动程序可能需要将原始的环绕声音频流拆分为两个流，一个用于每个编解码器。 通过使用[ **SetDmaEngineState** ](https://msdn.microsoft.com/library/windows/hardware/ff537889)例程来启动和停止更多信息流，两个流可以保持同步。

允许按甚至几个示例超出同步在两个流可能会导致不需要的音频项目。

[ **SetDmaEngineState** ](https://msdn.microsoft.com/library/windows/hardware/ff537889)例程是 HD 音频 DDI 的这两个版本中可用。

UAA HD Audio 类驱动程序不执行编解码器组合。

 

 




