---
title: KSPROPSETID \_ AudioModule
description: '\_音频驱动程序使用 KSPROPSETID AudioModule 属性集来检索音频模块列表。'
ms.assetid: 6F167E5E-CA11-45F3-BF21-6B9A3F90DB9F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c15321545252a49f41793b03c08c7037ec5bf7b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211469"
---
# <a name="kspropsetid_audiomodule"></a>KSPROPSETID \_ AudioModule


音频驱动程序使用 **KSPROPSETID \_ AudioModule** 属性集来检索音频模块列表。

*Ksmedia*头文件定义**KSPROPSETID \_ AudioModule**属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioModule \
    0xc034fdb0, 0xff75, 0x47c8, 0xaa, 0x3c, 0xee, 0x46, 0x71, 0x6b, 0x50, 0xc6
DEFINE_GUIDSTRUCT("C034FDB0-FF75-47C8-AA3C-EE46716B50C6", KSPROPSETID_AudioModule);
#define KSPROPSETID_AudioModule DEFINE_GUIDNAMED(KSPROPSETID_AudioModule)
```

**KSPROPSETID \_ AudioModule**属性集包含以下 KS 属性。

[**KSPROPERTY \_ AUDIOMODULE \_ 描述符**](ksproperty-audiomodule-descriptors.md)

[**KSPROPERTY \_ AUDIOMODULE \_ 命令**](ksproperty-audiomodule-command.md)

[**KSPROPERTY \_ AUDIOMODULE \_ 通知 \_ 设备 \_ ID**](ksproperty-audiomodule-notification-device-id.md)

此属性名称是在 [**KSPROPERTY \_ AUDIOMODULE**](ksproperty-audiomodule.md) 枚举中定义的。

有关音频模块的详细信息，请参阅 [实现音频模块发现](./implementing-audio-module-communication.md)。

 

