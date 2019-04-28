---
title: 避免数据复制
description: 避免数据复制
ms.assetid: bf4dab5e-5800-4888-af96-68a152ac5e39
keywords:
- 数据复制 WDK 音频
- 将音频数据复制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf46bb249d2b66574910651a6c88f0cb491f197
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333913"
---
# <a name="avoiding-data-copying"></a>避免数据复制


## <span id="avoiding_data_copying"></span><span id="AVOIDING_DATA_COPYING"></span>


可以通过设计音频硬件，以避免不必要的数据复制来提高驱动程序性能。

您可以获得最佳结果，通过实现您的硬件来执行，则返回 true 散播-聚集 DMA 和通过编写 WavePci 微型端口驱动程序，以管理硬件。 你的设备可以直接访问播放数据缓冲区或空记录的缓冲区的任意位置在系统内存中。 这消除了大量不必要的软件干预和耗时的数据复制。

如果您正在设计 WaveCyclic 设备，但是，可以改进其性能，从而其硬件缓冲区直接访问系统内存。 这消除了从中间缓冲区在系统内存中复制数据的开销。

此外，如果你的设备不符合标准的 WDM 音频格式的信道排序需要的音频格式，该驱动程序可能需要中间缓冲区中执行的每个音频帧的就地转换之前硬件可以对其进行处理。 这可能会降低性能。 有关其他信息，请参阅标题为多个声道音频数据和批文件的白皮书[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

 

 




