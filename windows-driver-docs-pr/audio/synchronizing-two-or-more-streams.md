---
title: 同步两个或多个流
description: 同步两个或多个流
ms.assetid: c25f4ca2-8a9f-43bc-a1bf-b71826b446ff
keywords:
- HD 音频，同步流
- 高清晰音频（HD 音频），同步流
- 同步流 WDK 音频
- 流同步 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3acb484f2d6bebc5e88848068c3c37b18bb6dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832340"
---
# <a name="synchronizing-two-or-more-streams"></a>同步两个或多个流


[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)例程将一个或多个 DMA 引擎的状态设置为以下其中一项：正在运行、已暂停、已停止或重置。 如果调用此例程指定了多个 DMA 引擎，则所有 DMA 引擎都将同步进行状态转换。

某些音频应用程序需要同步一组流。 例如，音频驱动程序可以使用编解码器组合来创建用于连接两个音频编解码器的逻辑环绕声设备：一个编解码器驱动前扬声器，另一个音频编解码器用于驱动背面的扬声器。 根据编解码器的功能，可能需要音频驱动程序将原始环绕声音频流拆分为两个流，每个流对应一个编解码器。 通过使用[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)例程来以统一方式启动和停止流，两个流可以保持同步。

即使少数示例允许两个流不同步，可能会导致意外的音频项目。

这两个版本的 HD audio DDI 都提供[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)例程。

UAA 高质音频类驱动程序不执行编解码器组合。

 

 




