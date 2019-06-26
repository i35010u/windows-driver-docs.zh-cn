---
title: KSPROPERTY\_调谐器\_扫描\_CAP
description: KSPROPERTY\_调谐器\_扫描\_CAPS 属性描述了优化的设备，包括设备支持的网络类型的扫描功能。
ms.assetid: 339d5f6b-81ac-419e-9821-a7f1642e1aa8
keywords:
- KSPROPERTY_TUNER_SCAN_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_SCAN_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1e0926dbd36b77b631b830c7e2ad5c6c120c4f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355965"
---
# <a name="kspropertytunerscancaps"></a>KSPROPERTY\_调谐器\_扫描\_CAP


KSPROPERTY\_调谐器\_扫描\_CAPS 属性描述了优化的设备，包括设备支持的网络类型的扫描功能。 此属性必须为 AVStream 优化微型驱动程序运行 Windows Vista 及更高版本的实现。

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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)"><strong>KSPROPERTY_TUNER_SCAN_CAPS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_CAPS_S</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_调谐器\_扫描\_CAPS\_S 结构，它指定支持的网络类型，以及是否驱动程序或固件的优化设备可以支持硬件辅助的扫描操作。

<a name="remarks"></a>备注
-------

该驱动程序应返回至少一个它支持的网络类型的以下 Guid。 在中定义这些 Guid *Bdamedia.h* ，应从引用*Bdamedia.h*。 有关这些 Guid 的详细信息，请参阅[广播网络类型 Guid](broadcast-network-type-guids.md)。

-   DIGITAL\_CABLE\_NETWORK\_TYPE

-   模拟\_电视\_网络\_类型

-   ANALOG\_AUXIN\_NETWORK\_TYPE

-   模拟\_FM\_网络\_类型

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_调谐器\_扫描\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

 

 






