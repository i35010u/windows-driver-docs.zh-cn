---
title: KSPROPERTY\_EXTDEVICE\_PORT
description: KSPROPERTY\_EXTDEVICE\_端口属性检索外部设备的端口类型。
ms.assetid: 7513c37f-0c93-4078-ba85-cbc98304880f
keywords:
- KSPROPERTY_EXTDEVICE_PORT 流式处理媒体设备
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
ms.openlocfilehash: 161dc349f23b6c96178ed44009c86be08cf6857a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373385"
---
# <a name="kspropertyextdeviceport"></a>KSPROPERTY\_EXTDEVICE\_PORT


KSPROPERTY\_EXTDEVICE\_端口属性检索外部设备的端口类型。

## <span id="ddk_ksproperty_extdevice_port_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_PORT_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，指定外部设备的连接端口。 例如 1394年或 USB。

<a name="remarks"></a>备注
-------

**DevPort** KSPROPERTY 成员\_EXTDEVICE\_S 结构指定外部设备的端口类型。 **DevPort**成员可能会设置为等于开发\_端口\_1394，开发人员\_端口\_USB，等等。这些标记中定义*xprtdefs.h* Microsoft DirectX SDK 中的文件。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

 

 






