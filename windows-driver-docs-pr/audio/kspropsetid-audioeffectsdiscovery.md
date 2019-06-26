---
title: KSPROPSETID\_AudioEffectsDiscovery
description: KSPROPSETID\_AudioEffectsDiscovery 属性集实现通过使用 Microsoft 的泛型代理音频处理对象 (APO) 的音频设备驱动程序。
ms.assetid: 68229885-1446-4BF0-B4E1-96A777006567
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 752ef27db4769a13239a2f9d782a46ed515833de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358721"
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

[**KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

此属性的名称中定义[ **KSPROPERTY\_AUDIOEFFECTSDISCOVERY** ](https://docs.microsoft.com/windows/desktop/api/msapofxproxy/ne-msapofxproxy-ksproperty_audioeffectsdiscovery)枚举。

 

 





