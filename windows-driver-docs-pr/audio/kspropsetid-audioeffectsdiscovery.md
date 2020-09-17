---
title: KSPROPSETID \_ AudioEffectsDiscovery
description: KSPROPSETID \_ AudioEffectsDiscovery 属性集由使用 Microsoft 的通用代理音频处理对象 (APO) 的音频设备驱动程序实现。
ms.assetid: 68229885-1446-4BF0-B4E1-96A777006567
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f44cc244ae6724faa9b52475b55ba330f29f223
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715032"
---
# <a name="kspropsetid_audioeffectsdiscovery"></a>KSPROPSETID \_ AudioEffectsDiscovery


**KSPROPSETID \_ AudioEffectsDiscovery**属性集由使用 Microsoft 的通用代理音频处理对象 (APO) 的音频设备驱动程序实现。

**KSPROPSETID \_** Windows 操作系统 Windows 8.1 和更高版本中提供了 AudioEffectsDiscovery。

*MsApoFxProxy*头文件定义**KSPROPSETID \_ AudioEffectsDiscovery**属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID \_ AudioEffectsDiscovery**属性集包含以下 KS 属性。

[**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST**](/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

此属性名称是在 [**KSPROPERTY \_ AUDIOEFFECTSDISCOVERY**](/windows/win32/api/msapofxproxy/ne-msapofxproxy-ksproperty_audioeffectsdiscovery) 枚举中定义的。

 

