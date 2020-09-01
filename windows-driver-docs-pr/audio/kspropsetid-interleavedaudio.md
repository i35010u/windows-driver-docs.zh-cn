---
title: KSPROPSETID \_ InterleavedAudio
description: KSPROPSETID \_ InterleavedAudio 属性集是由音频设备驱动程序实现的，这些驱动程序希望提供有关环回音频和捕获音频交叉的额外信息。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 51a61a8da27bcca39b9262ba3eca90b475357ee5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208845"
---
# <a name="kspropsetid_interleavedaudio"></a>KSPROPSETID \_ InterleavedAudio

**KSPROPSETID \_ InterleavedAudio**属性集是由音频设备驱动程序实现的，这些驱动程序需要包含有关在音频流中交叉环回音频和捕获音频的额外信息。

**KSPROPSETID \_InterleavedAudio** 适用于 windows 10 版本19H1 和更高版本的 windows。

*Ksmedia*头文件定义**KSPROPSETID \_ InterleavedAudio**属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_InterleavedAudio\
    0xe9ebe550, 0xd619, 0x4c0a, 0x97, 0x6b, 0x70, 0x62, 0x32, 0x2b, 0x30, 0x6
DEFINE_GUIDSTRUCT("E9EBE550-D619-4C0A-976B-7062322B3006", KSPROPSETID_InterleavedAudio);
#define KSPROPSETID_InterleavedAudio DEFINE_GUIDNAMED(KSPROPSETID_InterleavedAudio)
```

**KSPROPSETID \_ InterleavedAudio**属性集包含以下 KS 属性。

[**KSPROPERTY \_ INTERLEAVEDAUDIO_FORMATINFORMATION**](ksproperty-interleavedaudio-formatinformation.md)

此属性名称是在 [**KSPROPERTY \_ INTERLEAVEDAUDIO**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_interleavedaudio) 枚举中定义的。