---
title: KSPROPSETID\_AudioEngine
description: KSPROPSETID\_AudioEngine 属性集包含的音频驱动程序可用于提供有关硬件音频引擎节点的详细信息的 KS 属性。
ms.assetid: F3155DF6-0710-4941-94DC-478A8F5DE8D1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eaf256d66414c9b410c0afff49867c50cbb221f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520178"
---
# <a name="kspropsetidaudioengine"></a>KSPROPSETID\_AudioEngine


**KSPROPSETID\_AudioEngine**属性集包含的音频驱动程序可用于提供有关硬件音频引擎节点的详细信息的 KS 属性。

**KSPROPSETID\_AudioEngine**是可用于 Windows 8 和更高版本的 Windows 操作系统。

时硬件解决方案支持音频卸载，硬件的音频驱动程序必须以特定方式公开其功能，以便在 Windows 8 用户模式音频堆栈可以发现这些功能并充分利用它们。

若要支持与 Windows 8 提供的音频卸载体系结构，硬件解决方案必须实现硬件音频引擎。 然后，此硬件的音频驱动程序必须将硬件音频引擎公开为流式处理 (KS) 节点中 KS 筛选器包含一个音频引擎内核。 目的就是新定义的节点类型[ **KSNODETYPE\_音频\_引擎**](ksnodetype-audio-engine.md)。 [ **KSPROPERTY\_AUDIOENGINE** ](ksproperty-audioengine.md)枚举用于表示新 KS 属性。

*Ksmedia.h*标头文件定义**KSPROPSETID\_AudioEngine**属性设置，如下所示：

``` syntax
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

**KSPROPSETID\_AudioEngine**属性集包含以下 KS 属性。

## <span id="wdk_kspropsetid_audioengine"></span><span id="WDK_KSPROPSETID_AUDIOENGINE"></span>


[**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**](ksproperty-audioengine-buffer-size-limits.md)

[**KSPROPERTY\_AUDIOENGINE\_描述符**](ksproperty-audioengine-descriptor.md)

[**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**](ksproperty-audioengine-deviceformat.md)

[**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**](ksproperty-audioengine-gfx-enable.md)

[**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**](ksproperty-audioengine-lfx-enable.md)

[**KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION**](ksproperty-audioengine-loopback-protection.md)

[**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**](ksproperty-audioengine-mixformat.md)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

在中定义这些属性名称[ **KSPROPERTY\_AUDIOENGINE** ](ksproperty-audioengine.md)枚举。

 

 





