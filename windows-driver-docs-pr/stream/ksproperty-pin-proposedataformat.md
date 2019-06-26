---
title: KSPROPERTY\_PIN\_PROPOSEDATAFORMAT
description: 客户端使用 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性来确定通过 pin 工厂实例化的插针是否支持特定的数据格式。
ms.assetid: f1657fd1-0988-48b8-95d0-c6026965848b
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT 流式处理媒体设备
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
ms.openlocfilehash: fb2303d96c56d882829e5cef47959b4aa04e16a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361071"
---
# <a name="kspropertypinproposedataformat"></a>KSPROPERTY\_PIN\_PROPOSEDATAFORMAT


客户端使用 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性来确定通过 pin 工厂实例化的插针是否支持特定的数据格式。

## <span id="ddk_ksproperty_pin_proposedataformat_ks"></span><span id="DDK_KSPROPERTY_PIN_PROPOSEDATAFORMAT_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY_PIN_PROPOSEDATAFORMAT 包括类型 KSDATAFORMAT，指定建议的数据格式的结构。 指定此属性使用的 KSP_PIN，其中该成员指定相关 pin 工厂。

KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 包含类型的结构[ **KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)，指定建议的数据格式。

[**KSPROPERTY\_类型\_获取**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)支持 Windows 7 和更高版本的 Windows 中。 在 Windows Vista **KSPROPERTY\_类型\_获取**是*不支持*。 

**KSPROPERTY_TYPE_GET**与此属性允许音频驱动程序对 pin 提供的默认数据格式有关的信息。 **KSPROPERTY_TYPE_GET**取决于您要为此属性实现，除非该驱动程序支持[ **KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)。 
 

KS 筛选器将返回状态\_成功时使用此属性的 KSPROPERTY_TYPE_SET，如果 pin 可以设置为或使用建议的数据格式打开。 如果 pin 不能设置为建议的数据格式，它返回 STATUS_NO_MATCH。 对于任何其他失败，返回相应的错误。 如果该驱动程序支持[ **KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)，此属性应返回 STATUS_SUCCESS，如果任何音频信号处理模式支持的格式。 


使用此属性使用 KSPROPERTY_TYPE_SET 实际上不会更改数据格式。 客户端使用[ **KSPROPERTY\_连接\_DATAFORMAT** ](ksproperty-connection-dataformat.md)若要更改的数据格式。 **KSPROPERTY_TYPE_SET**取决于您要为此属性实现。


<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)
 
[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)

[**KS 属性**](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/ks-properties)

[**KSPROPERTY\_TYPE\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)
 
[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)





