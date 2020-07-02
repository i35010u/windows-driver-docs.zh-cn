---
title: KSPROPERTY \_ PIN \_ MODEDATAFORMATS
description: 客户端使用 KSPROPERTY_PIN_MODEDATAFORMATS 属性为 pin 工厂实例化的每个受支持的端口检索支持的格式列表。
ms.assetid: AD028946-2E6C-4385-B336-657FA1743EA8
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
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: d25a1ddec24f8ddee5e150acaa9f58e89e3cef5a
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85835150"
---
# <a name="ksproperty_pin_modedataformats"></a>KSPROPERTY \_ PIN \_ MODEDATAFORMATS

客户端使用**KSPROPERTY \_ 引脚 \_ MODEDATAFORMATS**属性为 pin 工厂实例化的 pin 的每个受支持的音频信号处理模式检索受支持格式的列表。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p>KSP_PIN，后跟模式 GUID</p></td>
<td><p>KSMULTIPLE_ITEM 结构，后跟一系列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a>结构</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

客户端使用此属性来检索由 pin 工厂实例化的 pin 所支持的特定音频信号处理模式所支持的格式列表。

使用[**KSP \_ PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) （后跟模式 guid）指定此属性，其中 KSP_PIN 成员和模式 guid 指定要为其返回格式列表的 PIN 工厂和模式。

**KSPROPERTY \_PIN \_ MODEDATAFORMATS**将支持的格式作为[**KSMULTIPLE \_ 项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构返回，其中，结构中的每一项都是一个 ULONGLONG，该结构中的每一项都是从 KSMULTIPLE_ITEM 开头的值到特定[KSDATAFORMAT 结构](ttps://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)的偏移量。
- KSMULTIPLE_ITEM：： Size 值包括 KSMULTIPLE_ITEM 的大小以及每个 KSDATAFORMAT 的大小。 
- KSMULTIPLE_ITEM：： Count 值包括每个 KSDATAFORMAT 的索引计数。

几乎在所有情况下，返回的 KSDATAFORMAT 结构实际上是 KSDATAFORMAT_WAVEFORMATEXTENSIBLE 或[KSDATAFORMAT_WAVEFORMATEX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)大小与匹配的结构。

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

有关详细信息，请参阅[可扩展波形格式说明符](https://docs.microsoft.com/windows-hardware/drivers/audio/extensible-wave-format-descriptors)。

## <a name="supported-mode-format-and-buffer-recommendations"></a>支持的模式格式和缓冲区建议

从 Windows 10 版本2004（20H1）开始，使用**KSPROPERTY \_ PIN \_ MODEDATAFORMATS**和[KSAUDIO_PACKETSIZE_CONSTRAINTS2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)是驱动程序报告受支持的音频信号处理模式格式和缓冲区大小约束的首选方法。 使用此方法可以有效地检索终结点流式处理功能，而无需创建多个流来发现终结点支持的格式和缓冲区大小。

### <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>从 Windows 10 版本2004（20H1）开始提供</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSP \_ PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSAUDIO_PACKETSIZE_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[KSDATAFORMAT_WAVEFORMATEX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)  
