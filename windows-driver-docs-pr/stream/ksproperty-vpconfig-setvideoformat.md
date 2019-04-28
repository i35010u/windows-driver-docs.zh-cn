---
title: KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT
description: KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT 属性设置的视频格式。 格式必须与其中一个匹配的早期 KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT Get 请求返回。
ms.assetid: f701ad32-ba85-4766-ac6b-11744af8fc0d
keywords:
- KSPROPERTY_VPCONFIG_SETVIDEOFORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETVIDEOFORMAT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 258e788592f849fd7484286e90be31a9242e4553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329969"
---
# <a name="kspropertyvpconfigsetvideoformat"></a>KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT


KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT 属性设置的视频格式。 格式必须与其中一个匹配的早期 KSPROPERTY\_VPCONFIG\_GETVIDEOFORMAT**获取**返回请求。

## <span id="ddk_ksproperty_vpconfig_setvideoformat_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETVIDEOFORMAT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550274" data-raw-source="[&lt;strong&gt;DDPIXELFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550274)"><strong>DDPIXELFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 DDPIXELFORMAT 结构，它指定要使用的视频格式。

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

[**DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)

 

 






