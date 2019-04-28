---
title: KSEVENTSETID\_LoopedStreaming
description: KSEVENTSETID\_LoopedStreaming
ms.assetid: 88baf1f0-d18f-4601-9ba3-fea957712cd6
keywords:
- KSEVENTSETID_LoopedStreaming
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 587158e7bee784222efa0bb8d0ae1e3d8ba14a2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333350"
---
# <a name="kseventsetidloopedstreaming"></a>KSEVENTSETID\_LoopedStreaming


此事件集旨在由系统仅供内部使用。

`KSEVENTSETID_LoopedStreaming`事件集定义中使用的音频流的事件循环缓冲区的位置。 一个循环的缓冲区就是类型的音频流的数据缓冲区[ **KSINTERFACE\_标准\_LOOPED\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff563381)。 通过位置事件，客户端时可以接收通知某个驱动程序的音频流到达循环缓冲区中的指定的位置。

在 Microsoft Windows Server 2003、 Windows XP、 Windows 2000、 Windows Me 和 Windows 98，实现对此事件集的驱动程序支持的唯一系统组件是 KMixer 和 PortCls （Kmixer.sys 和 Portcls.sys）。 DirectSound (Dsound.dll) 是使用作为客户端设置此事件的唯一系统组件。 自定义音频驱动程序通常不会实现对此事件集的支持。

在 Windows Vista 及更高版本，没有任何系统组件使用或支持`KSEVENTSETID_LoopedStreaming`事件集。

在此集中的事件项指定为 KSEVENT\_LOOPEDSTREAMING 枚举值。

在此集中的唯一事件是[ **KSEVENT\_LOOPEDSTREAMING\_位置**](ksevent-loopedstreaming-position.md)。

 

 





