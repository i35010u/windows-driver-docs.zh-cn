---
title: KSPROPERTY \_ EXTDEVICE \_ 端口
description: KSPROPERTY \_ EXTDEVICE \_ port 属性检索外部设备的端口类型。
ms.assetid: 7513c37f-0c93-4078-ba85-cbc98304880f
keywords:
- KSPROPERTY_EXTDEVICE_PORT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_PORT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f27c06ecf909637c4ec95496c6217be1c98cd46
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185717"
---
# <a name="ksproperty_extdevice_port"></a>KSPROPERTY \_ EXTDEVICE \_ 端口


KSPROPERTY \_ EXTDEVICE \_ port 属性检索外部设备的端口类型。

## <span id="ddk_ksproperty_extdevice_port_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_PORT_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个指定外部设备的连接端口的 ULONG。 例如1394或 USB。

<a name="remarks"></a>备注
-------

KSPROPERTY **DevPort** \_ EXTDEVICE S 结构的 DevPort 成员 \_ 指定外部设备的端口类型。 **DevPort**成员可设置为等于开发 \_ 端口 \_ 1394、开发 \_ 端口 \_ USB 等。这些令牌在 Microsoft DirectX SDK 中的*xprtdefs*文件中定义。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTDEVICE \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

