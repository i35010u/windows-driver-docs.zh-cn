---
title: KSPROPSETID \_ SoundDetector
description: 了解 "KSPROPSETID_SoundDetector" 属性集。 此设置包括 "KSPROPERTY \_ SOUNDDETECTOR \_ " 和 " \_ 模式" 和 \_ MATCHRESULT 属性。
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41a5f23efea3abc2b5e1b752b3de22055a431780
ms.sourcegitcommit: 2aedb606f9f14e74687f0d3da60e14fc6ffffa7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91544330"
---
# <a name="kspropsetid_sounddetector"></a>KSPROPSETID \_ SoundDetector


`KSPROPSETID_SoundDetector`属性集包含的属性用于为也支持检测程序的音频捕获设备注册筛选器。 该筛选器具有具有 pin 类别 **KSNODETYPE \_ AUDIO \_ KEYWORDDETECTOR**的 KS pin 工厂。 给定 KS 筛选器实例中不能有多个具有此 KS pin 类别的 pin 工厂。

此集中的属性项由 [**KSPROPERTY \_ SOUNDDETECTOR**](ksproperty-sounddetector.md) 枚举值指定，如标头文件 *ksmedia*中所定义。

标头文件定义 **KSPROPSETID \_ SoundDetector** 属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_SoundDetector\
    0x113c425e, 0xfd17, 0x4057, 0xb4, 0x22, 0xed, 0x40, 0x74, 0xf1, 0xaf, 0xdf
DEFINE_GUIDSTRUCT("113C425E-FD17-4057-B422-ED4074F1AFDF", KSPROPSETID_SoundDetector);
#define KSPROPSETID_SoundDetector DEFINE_GUIDNAMED(KSPROPSETID_SoundDetector)
```

`KSPROPSETID_SoundDetector`属性集包含以下属性：

-   [**KSPROPERTY \_ SOUNDDETECTOR \_**](ksproperty-sounddetector-armed.md)

-   [**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

-   [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md)

-   [**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

 

 





