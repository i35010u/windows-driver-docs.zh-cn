---
title: KSEVENTSETID \_ AudioControlChange
description: KSEVENTSETID \_ AudioControlChange
keywords:
- KSEVENTSETID_AudioControlChange
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68e3f84f1bd928c835a82f10087af43315b9d2a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784679"
---
# <a name="kseventsetid_audiocontrolchange"></a>KSEVENTSETID \_ AudioControlChange


## <span id="ddk_kseventsetid_audiocontrolchange_ks"></span><span id="DDK_KSEVENTSETID_AUDIOCONTROLCHANGE_KS"></span>


`KSEVENTSETID_AudioControlChange`当微型端口驱动程序检测到[硬件事件](./hardware-events.md)（这是对硬件卷控制旋钮、静音开关或其他类型手动控制的更改）时，将使用该事件集通知客户端。

此集中的事件项被指定为 KSEVENT \_ 音频 \_ 控件 \_ 更改枚举值。

此集中的唯一事件是 [**KSEVENT \_ 控件 \_ 更改**](ksevent-control-change.md)。

 

