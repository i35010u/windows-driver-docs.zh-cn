---
title: 已卸载音频的故障报告
description: 本主题介绍具有与硬件卸载音频流相关的报告干扰错误时，必须使用的音频驱动程序的机制。
ms.assetid: 9FF2A5D6-9382-4EE6-AA21-DCF47210F73B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7972a8fad43d01b3e25f2e34549b5cb0739e1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360016"
---
# <a name="glitch-reporting-for-offloaded-audio"></a>已卸载音频的故障报告


本主题介绍具有与硬件卸载音频流相关的报告干扰错误时，必须使用的音频驱动程序的机制。

时音频驱动程序检测到干扰错误，它必须引发一个事件跟踪 Windows (ETW) 事件以报告的错误。 此事件应包括小问题，以及使用的音频流的 DMA 缓冲区的相关信息的原因。

以下枚举显示已为要用于故障错误报告的音频驱动程序定义的事件。

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

有关此枚举的详细信息，请参阅[ **EPcMiniportEngineEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-epcminiportengineevent)。

有关如何开发驱动程序可以处理硬件卸载音频流的详细信息，请参阅[驱动程序实现细节](driver-implementation-details.md)。

 

 




