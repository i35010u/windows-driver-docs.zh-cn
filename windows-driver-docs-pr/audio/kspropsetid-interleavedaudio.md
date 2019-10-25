---
title: KSPROPSETID\_InterleavedAudio
description: KSPROPSETID\_InterleavedAudio 属性集是由音频设备驱动程序实现的，这些驱动程序希望提供有关环回音频和捕获音频交叉的额外信息。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c2c5d8aed23f5233c94e2a5d5e58051425d15e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832673"
---
# <a name="kspropsetid_interleavedaudio"></a>KSPROPSETID\_InterleavedAudio

**KSPROPSETID\_InterleavedAudio**属性集是由音频设备驱动程序实现的，这些驱动程序希望包含有关音频流中的环回音频交叉和捕获音频的额外信息。

**KSPROPSETID\_InterleavedAudio**适用于 windows 10 版本19H1 和更高版本的 windows。

*Ksmedia*头文件定义**KSPROPSETID\_InterleavedAudio**属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_InterleavedAudio\
    0xe9ebe550, 0xd619, 0x4c0a, 0x97, 0x6b, 0x70, 0x62, 0x32, 0x2b, 0x30, 0x6
DEFINE_GUIDSTRUCT("E9EBE550-D619-4C0A-976B-7062322B3006", KSPROPSETID_InterleavedAudio);
#define KSPROPSETID_InterleavedAudio DEFINE_GUIDNAMED(KSPROPSETID_InterleavedAudio)
```

**KSPROPSETID\_InterleavedAudio**属性集包含以下 KS 属性。

[**KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**](ksproperty-interleavedaudio-formatinformation.md)

此属性名称是在[**KSPROPERTY\_INTERLEAVEDAUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_interleavedaudio)枚举中定义的。
