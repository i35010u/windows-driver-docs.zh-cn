---
title: KSPROPSETID \_ AudioEffectsDiscovery
description: KSPROPSETID \_ AudioEffectsDiscovery 属性集由使用 Microsoft 的通用代理音频处理对象 (APO) 的音频设备驱动程序实现。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1375df288ccec0c05f9d6e9786486f7bc378364
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801119"
---
# <a name="kspropsetid_audioeffectsdiscovery"></a>KSPROPSETID \_ AudioEffectsDiscovery


**KSPROPSETID \_ AudioEffectsDiscovery** 属性集由使用 Microsoft 的通用代理音频处理对象 (APO) 的音频设备驱动程序实现。

**KSPROPSETID \_** Windows 操作系统 Windows 8.1 和更高版本中提供了 AudioEffectsDiscovery。

*MsApoFxProxy* 头文件定义 **KSPROPSETID \_ AudioEffectsDiscovery** 属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID \_ AudioEffectsDiscovery** 属性集包含以下 KS 属性。

[**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST**](./ksproperty-audioeffectsdiscovery-effectslist.md)

此属性名称是在 [**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY**](/windows/win32/api/msapofxproxy/ne-msapofxproxy-ksproperty_audioeffectsdiscovery) 枚举中定义的。

 

