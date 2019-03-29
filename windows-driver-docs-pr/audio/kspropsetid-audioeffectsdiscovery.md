---
title: KSPROPSETID\_AudioEffectsDiscovery
description: KSPROPSETID\_AudioEffectsDiscovery 属性集实现通过使用 Microsoft 的泛型代理音频处理对象 (APO) 的音频设备驱动程序。
ms.assetid: 68229885-1446-4BF0-B4E1-96A777006567
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b1c2797c662fae927f8215feba171fa642f5ae1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563160"
---
# <a name="kspropsetidaudioeffectsdiscovery"></a>KSPROPSETID\_AudioEffectsDiscovery


**KSPROPSETID\_AudioEffectsDiscovery**属性集实现通过使用 Microsoft 的泛型代理音频处理对象 (APO) 的音频设备驱动程序。

**KSPROPSETID\_AudioEffectsDiscovery**是可用于 Windows 8.1 和更高版本的 Windows 操作系统。

*MsApoFxProxy.h*标头文件定义**KSPROPSETID\_AudioEffectsDiscovery**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID\_AudioEffectsDiscovery**属性集包含以下 KS 属性。

[**KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST**](https://msdn.microsoft.com/library/windows/hardware/dn457706)

此属性的名称中定义[ **KSPROPERTY\_AUDIOEFFECTSDISCOVERY** ](https://msdn.microsoft.com/library/windows/hardware/dn457705)枚举。

 

 





