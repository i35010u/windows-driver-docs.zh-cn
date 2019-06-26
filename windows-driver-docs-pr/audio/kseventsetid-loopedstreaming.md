---
title: KSEVENTSETID\_LoopedStreaming
description: KSEVENTSETID\_LoopedStreaming
ms.assetid: 88baf1f0-d18f-4601-9ba3-fea957712cd6
keywords:
- KSEVENTSETID_LoopedStreaming
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39ee5d32aea060207605cbaafd9c484e98007ebe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359789"
---
# <a name="kseventsetidloopedstreaming"></a>KSEVENTSETID\_LoopedStreaming


此事件集旨在由系统仅供内部使用。

`KSEVENTSETID_LoopedStreaming`事件集定义中使用的音频流的事件循环缓冲区的位置。 一个循环的缓冲区就是类型的音频流的数据缓冲区[ **KSINTERFACE\_标准\_LOOPED\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)。 通过位置事件，客户端时可以接收通知某个驱动程序的音频流到达循环缓冲区中的指定的位置。

在 Microsoft Windows Server 2003、 Windows XP、 Windows 2000、 Windows Me 和 Windows 98，实现对此事件集的驱动程序支持的唯一系统组件是 KMixer 和 PortCls （Kmixer.sys 和 Portcls.sys）。 DirectSound (Dsound.dll) 是使用作为客户端设置此事件的唯一系统组件。 自定义音频驱动程序通常不会实现对此事件集的支持。

在 Windows Vista 及更高版本，没有任何系统组件使用或支持`KSEVENTSETID_LoopedStreaming`事件集。

在此集中的事件项指定为 KSEVENT\_LOOPEDSTREAMING 枚举值。

在此集中的唯一事件是[ **KSEVENT\_LOOPEDSTREAMING\_位置**](ksevent-loopedstreaming-position.md)。

 

 





