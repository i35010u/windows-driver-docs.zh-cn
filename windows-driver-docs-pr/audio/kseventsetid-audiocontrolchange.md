---
title: KSEVENTSETID \_ AudioControlChange
description: KSEVENTSETID \_ AudioControlChange
ms.assetid: 5189c284-d53a-4fc4-981c-7d6b3851dab1
keywords:
- KSEVENTSETID_AudioControlChange
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ec40b514bfc1e33c178093ba0db4ab7cc547b8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209031"
---
# <a name="kseventsetid_audiocontrolchange"></a>KSEVENTSETID \_ AudioControlChange


## <span id="ddk_kseventsetid_audiocontrolchange_ks"></span><span id="DDK_KSEVENTSETID_AUDIOCONTROLCHANGE_KS"></span>


`KSEVENTSETID_AudioControlChange`当微型端口驱动程序检测到[硬件事件](./hardware-events.md)（这是对硬件卷控制旋钮、静音开关或其他类型手动控制的更改）时，将使用该事件集通知客户端。

此集中的事件项被指定为 KSEVENT \_ 音频 \_ 控件 \_ 更改枚举值。

此集中的唯一事件是 [**KSEVENT \_ 控件 \_ 更改**](ksevent-control-change.md)。

 

