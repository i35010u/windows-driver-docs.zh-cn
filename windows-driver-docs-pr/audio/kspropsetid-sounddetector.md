---
title: KSPROPSETID\_SoundDetector
description: .
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f43a3289241254c514a0b1ae2964e04fd225f74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541513"
---
# <a name="kspropsetidsounddetector"></a>KSPROPSETID\_SoundDetector


`KSPROPSETID_SoundDetector`属性集包含用于注册还支持检测程序的音频捕获设备的筛选器的属性。 筛选器可以具有 pin 类别 KS pin 工厂**KSNODETYPE\_音频\_KEYWORDDETECTOR**。 不能有多个 pin 工厂给定 KS 筛选器实例中具有此 KS pin 类别。

指定在此集中的属性项[ **KSPROPERTY\_SOUNDDETECTOR** ](ksproperty-sounddetector.md)枚举值，标头文件中定义*ksmedia.h*。

标头文件定义**KSPROPSETID\_SoundDetector**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_SoundDetector\
    0x113c425e, 0xfd17, 0x4057, 0xb4, 0x22, 0xed, 0x40, 0x74, 0xf1, 0xaf, 0xdf
DEFINE_GUIDSTRUCT("113C425E-FD17-4057-B422-ED4074F1AFDF", KSPROPSETID_SoundDetector);
#define KSPROPSETID_SoundDetector DEFINE_GUIDNAMED(KSPROPSETID_SoundDetector)
```

`KSPROPSETID_SoundDetector`属性集包含以下属性：

-   [**KSPROPERTY\_SOUNDDETECTOR\_ARMED**](ksproperty-sounddetector-armed.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

 

 





