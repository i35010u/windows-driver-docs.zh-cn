---
title: KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP
description: KSPROPERTY \_ 调谐器 \_ SCAN \_ cap 属性介绍了优化设备的扫描功能，包括设备支持的网络类型。
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
ms.openlocfilehash: 8817cfca2e67c6e803b6bfde47d13d2c41c8388e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788163"
---
# <a name="ksproperty_tuner_scan_caps"></a>KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP


KSPROPERTY \_ 调谐器 \_ SCAN \_ cap 属性介绍了优化设备的扫描功能，包括设备支持的网络类型。 必须为在 Windows Vista 和更高版本上运行的 AVStream 优化微型驱动程序实现此属性。

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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)"><strong>KSPROPERTY_TUNER_SCAN_CAPS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_CAPS_S</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ 调谐器 \_ 扫描 \_ cap \_ S 结构，该结构指定支持的网络类型以及优化设备的驱动程序或固件是否可以支持硬件辅助扫描操作。

<a name="remarks"></a>备注
-------

驱动程序应至少为其支持的网络类型返回以下 Guid 之一。 这些 Guid 是在 *Bdamedia* 中定义的，应从 *Bdamedia* 引用。 有关这些 Guid 的详细信息，请参阅 [广播网络类型 guid](broadcast-network-type-guids.md)。

-   数字 \_ 有线 \_ 网络 \_ 类型

-   模拟 \_ 电视 \_ 网络 \_ 类型

-   模拟 \_ AUXIN \_ 网络 \_ 类型

-   模拟 \_ FM \_ 网络 \_ 类型

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

