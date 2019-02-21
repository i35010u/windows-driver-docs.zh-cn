---
title: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE
description: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE 属性指定基于像素格式的最大像素费率，它指定维度 （通过高度的宽度） 的连接。
ms.assetid: 5a1e70b6-32ab-4a6c-82f7-3e6e828262a4
keywords:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8c86184f23a9afccecaea0764e77d5f67799e38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544594"
---
# <a name="kspropertyvpconfigmaxpixelrate"></a>KSPROPERTY\_VPCONFIG\_MAXPIXELRATE


KSPROPERTY\_VPCONFIG\_MAXPIXELRATE 属性指定基于像素格式的最大像素费率，它指定维度 （通过高度的宽度） 的连接。

## <span id="ddk_ksproperty_vpconfig_maxpixelrate_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_MAXPIXELRATE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567234" data-raw-source="[&lt;strong&gt;KSVPMAXPIXELRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567234)"><strong>KSVPMAXPIXELRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种 KSVPMAXPIXELRATE 结构描述的宽度、 高度和最大每秒的视频端口支持的像素的数目。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSVPMAXPIXELRATE**](https://msdn.microsoft.com/library/windows/hardware/ff567234)

 

 






