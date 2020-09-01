---
title: 避免数据复制
description: 避免数据复制
ms.assetid: bf4dab5e-5800-4888-af96-68a152ac5e39
keywords:
- 数据复制 WDK 音频
- 复制音频数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0df62075929112477dbdfee7bc6697282af3ef25
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208251"
---
# <a name="avoiding-data-copying"></a>避免数据复制

## <span id="avoiding_data_copying"></span><span id="AVOIDING_DATA_COPYING"></span>

你可以通过设计音频硬件来提高驱动程序性能，以避免不必要的数据复制。

通过实现硬件以执行真正的散播/聚集 DMA，并通过编写 WavePci 微型端口驱动程序来管理硬件，可以获得最佳结果。 然后，设备可以在系统内存中任何位置直接访问播放数据缓冲区或空的记录缓冲区。 这消除了大量不必要的软件干预和耗时的数据复制。

但是，如果要设计 WaveCyclic 设备，则可以通过将其硬件缓冲区作为系统内存直接访问来改善其性能。 这消除了在系统内存中从中间缓冲区复制数据的开销。

此外，如果你的设备需要的音频格式的通道顺序与标准 WDM 音频格式不兼容，则驱动程序可能必须在中间缓冲区中的每个音频帧执行就地转换，然后硬件才能处理。 这可能会降低性能。 有关其他信息，请参阅 [多通道音频数据和波形文件](/previous-versions/windows/hardware/design/dn653308(v=vs.85))。