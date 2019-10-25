---
title: KSPROPERTY\_调谐器\_扫描\_CAP
description: KSPROPERTY\_调谐器\_扫描\_CAP 属性描述优化设备的扫描功能，包括设备支持的网络类型。
ms.assetid: 339d5f6b-81ac-419e-9821-a7f1642e1aa8
keywords:
- KSPROPERTY_TUNER_SCAN_CAPS 流媒体设备
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
ms.openlocfilehash: 2e19f33c1b54b58f29f1840015aecc4aea0b3a2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837906"
---
# <a name="ksproperty_tuner_scan_caps"></a>KSPROPERTY\_调谐器\_扫描\_CAP


KSPROPERTY\_调谐器\_扫描\_CAP 属性描述优化设备的扫描功能，包括设备支持的网络类型。 必须为在 Windows Vista 和更高版本上运行的 AVStream 优化微型驱动程序实现此属性。

### <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)"><strong>KSPROPERTY_TUNER_SCAN_CAPS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_CAPS_S</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSPROPERTY\_调谐器\_扫描\_CAP\_S 结构，该结构指定支持的网络类型以及优化设备的驱动程序或固件是否可以支持硬件辅助扫描运算符.

<a name="remarks"></a>备注
-------

驱动程序应至少为其支持的网络类型返回以下 Guid 之一。 这些 Guid 是在*Bdamedia*中定义的，应从*Bdamedia*引用。 有关这些 Guid 的详细信息，请参阅[广播网络类型 guid](broadcast-network-type-guids.md)。

-   数字\_电缆\_网络\_类型

-   模拟\_TV\_网络\_类型

-   模拟\_AUXIN\_网络\_类型

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
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_调谐器\_扫描\_CAP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

 

 






