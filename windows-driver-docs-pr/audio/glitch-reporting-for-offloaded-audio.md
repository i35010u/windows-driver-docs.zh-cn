---
title: 已卸载音频的故障报告
description: 本主题说明音频驱动程序必须在与硬件卸载的音频流的连接中报告 glitching 错误时必须使用的机制。
ms.assetid: 9FF2A5D6-9382-4EE6-AA21-DCF47210F73B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f21808c503a59cdf50e61a5fd8b6ec55e7226e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209207"
---
# <a name="glitch-reporting-for-offloaded-audio"></a>已卸载音频的故障报告


本主题说明音频驱动程序必须在与硬件卸载的音频流的连接中报告 glitching 错误时必须使用的机制。

当音频驱动程序检测到 glitching 错误时，它必须引发 Windows (ETW 事件跟踪) 事件来报告错误。 此事件应包括故障原因，以及有关音频流使用的 DMA 缓冲区的信息。

下面的枚举显示了为音频驱动程序定义的用于错误报告的事件。

```ManagedCPlusPlus
typedef enum 
{
    eMINIPORT_IHV_DEFINED = 0, 
    eMINIPORT_BUFFER_COMPLETE,
    eMINIPORT_PIN_STATE,
    eMINIPORT_GET_STREAM_POS,
    eMINIPORT_SET_WAVERT_BUFFER_WRITE_POS,
    eMINIPORT_GET_PRESENTATION_POS,
    eMINIPORT_PROGRAM_DMA,
    eMINIPORT_GLITCH_REPORT
} EPcMiniportEngineEvent;
```

有关此枚举的详细信息，请参阅 [**EPcMiniportEngineEvent**](/windows-hardware/drivers/ddi/portcls/ne-portcls-epcminiportengineevent)。

有关如何开发可处理硬件卸载音频流的驱动程序的详细信息，请参阅 [驱动程序实现细节](driver-implementation-details.md)。

 

