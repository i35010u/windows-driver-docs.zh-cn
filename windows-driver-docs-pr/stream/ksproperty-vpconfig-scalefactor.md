---
title: KSPROPERTY\_VPCONFIG\_SCALEFACTOR
description: KSPROPERTY\_VPCONFIG\_SCALEFACTOR 属性设置的视频端口维度对用户定义的规范。
ms.assetid: 0fbfedc8-9dff-4c7c-910f-507b84614e47
keywords:
- KSPROPERTY_VPCONFIG_SCALEFACTOR 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SCALEFACTOR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed1e335fe0c3261e10d10b09d0a66e7eac8ce10a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386497"
---
# <a name="kspropertyvpconfigscalefactor"></a>KSPROPERTY\_VPCONFIG\_SCALEFACTOR


KSPROPERTY\_VPCONFIG\_SCALEFACTOR 属性设置的视频端口维度对用户定义的规范。

## <span id="ddk_ksproperty_vpconfig_scalefactor_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SCALEFACTOR_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567268" data-raw-source="[&lt;strong&gt;KS_AMVPSIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567268)"><strong>KS_AMVPSIZE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_AMVPSIZE 结构，它指定的宽度和高度的视频端口。

<a name="remarks"></a>备注
-------

此属性由 KSPROPSETID\_VPVBIConfig，属性的所有请求必须都返回状态\_不\_实现。

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

[**KS\_AMVPSIZE**](https://msdn.microsoft.com/library/windows/hardware/ff567268)

 

 






