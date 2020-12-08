---
title: KSPROPSETID \_ AudioEngine
description: KSPROPSETID \_ AudioEngine 属性集包含 KS 属性，音频驱动程序可以使用这些属性来提供有关硬件音频引擎节点的详细信息。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ec9637a1c823411aa0a88ee66e124a18a57eb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801117"
---
# <a name="kspropsetid_audioengine"></a>KSPROPSETID \_ AudioEngine


**KSPROPSETID \_ AudioEngine** 属性集包含 KS 属性，音频驱动程序可以使用这些属性来提供有关硬件音频引擎节点的详细信息。

**KSPROPSETID \_** Windows 8 及更高版本的 windows 操作系统中提供了 AudioEngine。

当硬件解决方案支持音频卸载时，硬件的音频驱动程序必须以特定的方式公开其功能，以便 Windows 8 用户模式音频堆栈可以发现这些功能并利用这些功能。

若要支持 Windows 8 随附的音频卸载体系结构，硬件解决方案必须实现硬件音频引擎。 然后，此硬件的音频驱动程序必须将硬件音频引擎公开为包含在 KS 筛选器中的音频引擎内核流式处理 (KS) 节点。 为此目的新定义的节点类型为 [**KSNODETYPE \_ AUDIO \_ ENGINE**](ksnodetype-audio-engine.md)。 [**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)枚举用于表示新的 KS 属性。

*Ksmedia* 头文件定义 **KSPROPSETID \_ AudioEngine** 属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

**KSPROPSETID \_ AudioEngine** 属性集包含以下 KS 属性。

## <span id="wdk_kspropsetid_audioengine"></span><span id="WDK_KSPROPSETID_AUDIOENGINE"></span>


[**KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](ksproperty-audioengine-buffer-size-limits.md)

[**KSPROPERTY \_ AUDIOENGINE \_ 描述符**](ksproperty-audioengine-descriptor.md)

[**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**](ksproperty-audioengine-deviceformat.md)

[**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE**](ksproperty-audioengine-gfx-enable.md)

[**KSPROPERTY \_ AUDIOENGINE \_ LFXENABLE**](ksproperty-audioengine-lfx-enable.md)

[**KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ 保护**](ksproperty-audioengine-loopback-protection.md)

[**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**](ksproperty-audioengine-mixformat.md)

[**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

[**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

这些属性名称是在 [**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md) 枚举中定义的。

 

 





