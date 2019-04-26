---
title: KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数
description: KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数属性指定的数字要应用于图像的缩放量。
ms.assetid: e566dd2b-d99a-4e7f-888e-f0f431618c2d
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 611cddf64c30e7fc4e4c52a87bb6400b614798cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327163"
---
# <a name="kspropertyvideoprocampdigitalmultiplier"></a>KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数


KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数属性指定的数字要应用于图像的缩放量。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的数字乘数设置长时间。 值指定数字的乘数值的相机应用于映像。

<a name="remarks"></a>备注
-------

在 set 请求时，客户端应提供中的数字的乘数值**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

若要确定设备支持的数字的乘数值的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构。

客户端时发出 get 请求，接收类型的值长数据类型位于**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

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

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 






