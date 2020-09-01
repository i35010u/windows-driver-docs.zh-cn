---
title: KSEVENTSETID \_ LoopedStreaming
description: KSEVENTSETID \_ LoopedStreaming
ms.assetid: 88baf1f0-d18f-4601-9ba3-fea957712cd6
keywords:
- KSEVENTSETID_LoopedStreaming
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a60171d9bf3c7a9ab24da9bf68e7a5349e1dde2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209025"
---
# <a name="kseventsetid_loopedstreaming"></a>KSEVENTSETID \_ LoopedStreaming


此事件集仅供系统内部使用。

`KSEVENTSETID_LoopedStreaming`事件集定义使用循环缓冲区的音频流中的位置事件。 循环缓冲区是 [**KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理**](../stream/ksinterface-standard-looped-streaming.md)类型的音频流的数据缓冲区。 通过位置事件，当音频流到达循环缓冲区中的指定位置时，客户端可以接收来自驱动程序的通知。

在 Microsoft Windows Server 2003、Windows XP、windows 2000、Windows Me 和 Windows 98 中，唯一实现此事件集的驱动程序支持的系统组件是 KMixer 和 PortCls ( # A0 和 Portcls.sys) 。 DirectSound ( # A0) 是使用此事件集作为客户端的唯一系统组件。 自定义音频驱动程序通常不实现对此事件集的支持。

在 Windows Vista 和更高版本中，系统组件不使用或不支持 `KSEVENTSETID_LoopedStreaming` 事件集。

此集中的事件项被指定为 KSEVENT \_ LOOPEDSTREAMING 枚举值。

此集中的唯一事件是 [**KSEVENT \_ LOOPEDSTREAMING \_ 位置**](ksevent-loopedstreaming-position.md)。

 

