---
title: 在格式标记与子格式 GUID 之间进行转换
description: 在格式标记与子格式 GUID 之间进行转换
ms.assetid: 299ad5d3-df62-41cf-a18f-daa83cc60ef3
keywords:
- 非 PCM 音频格式 WDK，子格式 GUID 转换
- subformat Guid WDK 音频
- 格式标记以及子 Guid 格式转换为
- 数据交集处理程序 WDK 音频，非 PCM 波形格式
- Guid WDK 音频
- wave 格式标记 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490bcf5702cf0dfadd51af6e15b47770e5883458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355584"
---
# <a name="converting-between-format-tags-and-subformat-guids"></a>在格式标记与子格式 GUID 之间进行转换


## <span id="converting_between_format_tags_and_subformat_guids"></span><span id="CONVERTING_BETWEEN_FORMAT_TAGS_AND_SUBFORMAT_GUIDS"></span>


用于处理非 PCM WAVE 的准则\_格式\_可扩展的格式为类似于由波形格式标记指定的非 PCM 格式。 具体而言，会出现一批\_格式\_可扩展格式应具有独立于 PCM 格式的工厂的 pin 工厂，它需要自己的数据范围的交集处理程序。

波形音频格式\_格式\_可扩展格式由中的 GUID 指定**子格式**的成员[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构。 每个已注册的波形格式标记具有相应的子格式定义由生成的 GUID\_WAVEFORMATEX\_中 Ksmedia.h GUID 宏。 例如，与批相对应的 GUID\_格式\_DOLBY\_AC3\_SPDIF 标记指定义\_WAVEFORMATEX\_GUID (WAVE\_格式\_DOLBY\_AC3\_SPDIF)。

从 Ksmedia.h 此代码片段演示如何定义新的 GUID 为 autoinitialized 静态变量：

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_WAVEFORMATEX \
 0x00000000L, 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
DEFINE_GUIDSTRUCT("00000000-0000-0010-8000-00aa00389b71", KSDATAFORMAT_SUBTYPE_WAVEFORMATEX);
#define KSDATAFORMAT_SUBTYPE_WAVEFORMATEX DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_WAVEFORMATEX)
```

从 Ksmedia.h 这些宏将转换之间波形格式标记和其关联的 Guid:

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

下面的代码示例综合了这些方法来创建子格式基于波形格式标记批的 GUID\_格式\_AC3\_SPDIF，其值 0x0092:

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

 

 




