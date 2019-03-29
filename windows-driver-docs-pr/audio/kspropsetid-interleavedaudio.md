---
title: KSPROPSETID\_InterleavedAudio
description: KSPROPSETID\_InterleavedAudio 属性集实现想要提供有关交错的环回音频的额外信息并捕获音频的音频设备驱动程序。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19699f56b023b94917203f51a7b3eb1279acef60
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136106"
---
# <a name="kspropsetidinterleavedaudio"></a>KSPROPSETID\_InterleavedAudio

**KSPROPSETID\_InterleavedAudio**由想要包含有关交错的环回音频的额外信息并捕获音频流中的音频的音频设备驱动程序实现的属性集。

**KSPROPSETID\_InterleavedAudio**是版本中提供的 Windows 10 版本 19 H 1 及更高版本的 Windows。

*Ksmedia.h*标头文件定义**KSPROPSETID\_InterleavedAudio**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_InterleavedAudio\
    0xe9ebe550, 0xd619, 0x4c0a, 0x97, 0x6b, 0x70, 0x62, 0x32, 0x2b, 0x30, 0x6
DEFINE_GUIDSTRUCT("E9EBE550-D619-4C0A-976B-7062322B3006", KSPROPSETID_InterleavedAudio);
#define KSPROPSETID_InterleavedAudio DEFINE_GUIDNAMED(KSPROPSETID_InterleavedAudio)
```

**KSPROPSETID\_InterleavedAudio**属性集包含以下 KS 属性。

[**KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**](ksproperty-interleavedaudio-formatinformation.md)

此属性的名称中定义[ **KSPROPERTY\_INTERLEAVEDAUDIO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_interleavedaudio)枚举。
