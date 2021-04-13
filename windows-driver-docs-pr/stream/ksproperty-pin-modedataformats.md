---
title: KSPROPERTY_PIN_MODEDATAFORMATS
description: 客户端使用 KSPROPERTY_PIN_MODEDATAFORMATS 属性为 pin 工厂实例化的每个受支持的端口检索支持的格式列表。
keywords:
- KSPROPERTY_PIN_MODEDATAFORMATS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MODEDATAFORMATS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 04/12/2021
ms.localizationpriority: medium
ms.openlocfilehash: 5317e2b771729c4a5c5127cd3ca5ef7d8c90413e
ms.sourcegitcommit: 022dc99fdf23dc3501a3cebeb3c0698d504e31c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107325030"
---
# <a name="ksproperty_pin_modedataformats"></a>KSPROPERTY_PIN_MODEDATAFORMATS

客户端使用  **KSPROPERTY_PIN_MODEDATAFORMATS** 属性为 pin 工厂实例化的 pin 的每个受支持的音频信号处理模式检索受支持格式的列表。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 否 | 筛选器 | **KSP_PIN**，后跟模式 GUID | **KSMULTIPLE_ITEM** 结构，后跟一系列 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构 |

## <a name="remarks"></a>注解

客户端使用此属性来检索由 pin 工厂实例化的 pin 所支持的特定音频信号处理模式所支持的格式列表。

使用 [**KSP_PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) 后跟模式 guid 指定此属性，其中 **KSP_PIN** 成员和模式 guid 指定要为其返回格式列表的 PIN 工厂和模式。

**KSPROPERTY_PIN_MODEDATAFORMATS** 以 [**KSMULTIPLE_ITEM**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构的形式返回支持的格式，其中，结构中的每一项都是一个 ULONGLONG，该结构中的每一项都是从 **KSMULTIPLE_ITEM** 开头的值到特定 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构的偏移量。

- **KSMULTIPLE_ITEM：： Size** 值包括 **KSMULTIPLE_ITEM** 的大小以及每个 **KSDATAFORMAT** 的大小。

- **KSMULTIPLE_ITEM：： Count** 值包括每个 **KSDATAFORMAT** 的索引计数。

几乎在所有情况下，返回的 **KSDATAFORMAT** 结构实际上是 **KSDATAFORMAT_WAVEFORMATEXTENSIBLE** 或 [**KSDATAFORMAT_WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 大小与匹配的结构。

例如，支持两种格式的 pin 工厂的值将如下所示。

```cpp
{
    // Example Property Value Result, with 2 formats
    // Size of the KSMULTIPLE_ITEM structure + Size of two ULONGLONG offset values + Size of first format + Size of second format
    sizeof(KSMULTIPLE_ITEM) + sizeof(ULONGLONG)*2 + (First KSDATAFORMAT::Size) + (Second KSDATAFORMAT::Size),
    // Number of formats being returned
    2,
    // Offset of the first format from the beginning of the Property Value
    (sizeof(KSMULTIPLE_ITEM) + 2 * sizeof(ULONGLONG)),
    // Offset of the second format from the beginning of the Property Value
    (sizeof(KSMULTIPLE_ITEM) + 2 * sizeof(ULONGLONG) + (First KSDATAFORMAT::Size),
    // First format structure
    {(First KSDATAFORMAT)},
    // Second format structure
    {(Second KSDATAFORMAT)}
}
```

有关详细信息，请参阅 [可扩展 Wave-Format 描述符](../audio/extensible-wave-format-descriptors.md)。

## <a name="supported-mode-format-and-buffer-recommendations"></a>支持的模式格式和缓冲区建议

从 Windows 10 版本2004开始，使用 **KSPROPERTY_PIN_MODEDATAFORMATS** 和 [**KSAUDIO_PACKETSIZE_CONSTRAINTS2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2) 是驱动程序报告受支持的音频信号处理模式格式和缓冲区大小约束的首选方法。 使用此方法可以有效地检索终结点流式处理功能，而无需创建多个流来发现终结点支持的格式和缓冲区大小。

## <a name="requirements"></a>要求

**版本：** 从 Windows 10 开始提供，版本2004

**标头：** ks .h (包含 ks .h) 

## <a name="see-also"></a>另请参阅

[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSAUDIO_PACKETSIZE_CONSTRAINTS2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[**KSDATAFORMAT_WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)
