---
title: 在格式标记与子格式 GUID 之间进行转换
description: 在格式标记与子格式 GUID 之间进行转换
keywords:
- 非 PCM 音频格式 WDK，subformat GUID 转换
- subformat Guid WDK 音频
- 转换格式标记和 subformat Guid
- 数据交集处理程序 WDK 音频，非 PCM 波浪格式
- Guid WDK 音频
- 波形格式标记 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c463ad5b99aa4ba691cacc674a4a89446650bdc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784897"
---
# <a name="converting-between-format-tags-and-subformat-guids"></a>在格式标记与子格式 GUID 之间进行转换


## <span id="converting_between_format_tags_and_subformat_guids"></span><span id="CONVERTING_BETWEEN_FORMAT_TAGS_AND_SUBFORMAT_GUIDS"></span>


处理非 PCM 波浪 \_ 格式的 \_ 可扩展格式的准则类似于波形格式标记指定的非 pcm 格式的规则。 具体而言，波形 \_ 格式的 \_ 可扩展格式应该具有独立于 PCM 格式的工厂的 pin 工厂，并且它需要自己的数据范围交集处理程序。

波形 \_ 格式可扩展格式的音频格式 \_ 由 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构的 **SubFormat** 成员中的 GUID 指定。 每个已注册的波形格式标记都有相应的 subformat GUID，它是由 \_ Ksmedia 中的 DEFINE WAVEFORMATEX \_ guid 宏生成的。 例如，波形 \_ 格式 \_ 杜比 \_ e-ac3 spdif 标记对应的 GUID \_ 定义为定义 \_ WAVEFORMATEX \_ GUID (WAVE \_ 格式 \_ 杜 \_ e-ac3 \_ SPDIF) 。

此 Ksmedia 中的代码片段演示了如何将新的 GUID 定义为 autoinitialized 静态变量：

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_WAVEFORMATEX \
 0x00000000L, 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
DEFINE_GUIDSTRUCT("00000000-0000-0010-8000-00aa00389b71", KSDATAFORMAT_SUBTYPE_WAVEFORMATEX);
#define KSDATAFORMAT_SUBTYPE_WAVEFORMATEX DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_WAVEFORMATEX)
```

Ksmedia 中的这些宏在 wave 格式标记与其关联 Guid 之间转换：

```cpp
#if !defined( DEFINE_WAVEFORMATEX_GUID )
#define DEFINE_WAVEFORMATEX_GUID(x) \
    (USHORT)(x), 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
#endif

#define INIT_WAVEFORMATEX_GUID(Guid, x) \
{ \
    *(Guid) = KSDATAFORMAT_SUBTYPE_WAVEFORMATEX; \
    (Guid)->Data1 = (USHORT)(x); \
}

#define IS_VALID_WAVEFORMATEX_GUID(Guid) \
    (!memcmp(((PUSHORT)&KSDATAFORMAT_SUBTYPE_WAVEFORMATEX) + 1, \
    ((PUSHORT)(Guid)) + 1, sizeof(GUID) - sizeof(USHORT)))

#define EXTRACT_WAVEFORMATEX_ID(Guid)(USHORT)((Guid)->Data1)
```

下面的示例代码结合了这些技术来创建基于波形格式标记波格式的 subformat GUID \_ \_ \_ ，e-ac3 SPDIF 的值为0x0092：

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF \
    DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)

DEFINE_GUIDSTRUCT("00000092-0000-0010-8000-00aa00389b71",
    KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF);

#define KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF \
    DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF)
...
INIT_WAVEFORMATEX_GUID(pMyGuid,myWaveFormatTag);
...
if (IS_VALID_WAVEFORMATEX_GUID(aWaveFormatExGuidPtr)) {
    aWaveFormatTag = EXTRACT_WAVEFORMATEX_ID(aWaveFormatExGuidPtr);
}
```

 

