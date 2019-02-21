---
title: KSPROPSETID\_AudioSignalProcessing
description: KSPROPSETID\_音频驱动程序用 AudioSignalProcessing 属性集来检索 pin 工厂所支持的音频信号处理模式的列表。
ms.assetid: D9EF0D65-4DCD-4936-B7AC-A17FA50D3AE7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1acdb33d84430f41eccc4114f33b1421d3df4b3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541453"
---
# <a name="kspropsetidaudiosignalprocessing"></a>KSPROPSETID\_AudioSignalProcessing


**KSPROPSETID\_AudioSignalProcessing**音频驱动程序使用属性集来检索 pin 工厂所支持的音频信号处理模式的列表。

*Ksmedia.h*标头文件定义**KSPROPSETID\_AudioSignalProcessing**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID\_AudioSignalProcessing**属性集包含以下 KS 属性。

[**KSPROPERTY\_AUDIOSIGNALPROCESSING\_模式**](ksproperty-audiosignalprocessing-modes.md)

此属性的名称中定义[ **KSPROPERTY\_AUDIOSIGNALPROCESSING** ](ksproperty-audiosignalprocessing.md)枚举。

 

 





