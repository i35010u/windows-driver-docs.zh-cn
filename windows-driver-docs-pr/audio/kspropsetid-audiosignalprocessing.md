---
title: KSPROPSETID \_ AudioSignalProcessing
description: '\_音频驱动程序使用 KSPROPSETID AudioSignalProcessing 属性集来检索 pin 工厂支持的音频信号处理模式的列表。'
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 303e74bfc59506cf97c1b9c2094139c46f12c8b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801109"
---
# <a name="kspropsetid_audiosignalprocessing"></a>KSPROPSETID \_ AudioSignalProcessing


音频驱动程序使用 **KSPROPSETID \_ AudioSignalProcessing** 属性集来检索 pin 工厂支持的音频信号处理模式的列表。

*Ksmedia* 头文件定义 **KSPROPSETID \_ AudioSignalProcessing** 属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID \_ AudioSignalProcessing** 属性集包含以下 KS 属性。

[**KSPROPERTY \_ AUDIOSIGNALPROCESSING \_ 模式**](ksproperty-audiosignalprocessing-modes.md)

此属性名称是在 [**KSPROPERTY \_ AUDIOSIGNALPROCESSING**](ksproperty-audiosignalprocessing.md) 枚举中定义的。

 

 





