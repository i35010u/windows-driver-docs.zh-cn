---
title: KSPROPERTY\_PIN\_PROPOSEDATAFORMAT
description: 客户端使用 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性来确定 pin 工厂实例化的 pin 是否支持特定的数据格式。
ms.assetid: f1657fd1-0988-48b8-95d0-c6026965848b
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 12/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: eabb47c31cfae10f60962a74ce70e42f81bfd602
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881893"
---
# <a name="ksproperty_pin_proposedataformat"></a>KSPROPERTY\_PIN\_PROPOSEDATAFORMAT

客户端使用 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性来确定 pin 工厂实例化的 pin 是否支持特定的数据格式。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

KSPROPERTY_PIN_PROPOSEDATAFORMAT 包括 KSDATAFORMAT 类型的结构，并指定建议的数据格式。 使用 KSP_PIN 指定此属性，其中成员指定相关的 PIN 工厂。

KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 包含[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)类型的结构，指定建议的数据格式。

Windows 7 和更高版本的 Windows 支持[**KSPROPERTY\_类型\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 。 在 Windows Vista KSPROPERTY 中，*不支持* **\_GET\_类型**。

使用此属性**KSPROPERTY_TYPE_GET**允许音频驱动程序提供有关 pin 的默认数据格式的信息。 **KSPROPERTY_TYPE_GET**对于此属性是可选的，除非该驱动程序支持[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)。

如果可以将 pin 设置为或使用建议的数据格式打开，则 KS 筛选器将返回状态\_KSPROPERTY_TYPE_SET 成功。 如果无法将 pin 设置为建议的数据格式，则它将返回 STATUS_NO_MATCH。 对于其他任何失败，将返回相应的错误。 如果驱动程序支持[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)，则此属性应返回 STATUS_SUCCESS 如果任何音频信号处理模式支持该格式。

使用带有此属性的 KSPROPERTY_TYPE_SET 实际上不会更改数据格式。 客户端使用[**KSPROPERTY\_连接\_DATAFORMAT**](ksproperty-connection-dataformat.md)来更改数据格式。 对于此属性， **KSPROPERTY_TYPE_SET**是可选的。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)

[**KS 属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)

[**KSPROPERTY\_类型\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)
