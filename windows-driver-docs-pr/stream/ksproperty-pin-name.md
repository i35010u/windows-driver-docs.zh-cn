---
title: KSPROPERTY\_PIN\_NAME
description: 客户端使用 KSPROPERTY\_PIN\_要检索的 pin 工厂注册表名称的名称。 这是已本地化的 Unicode 字符串。
ms.assetid: 763c3116-95f5-4d32-8c46-d8d91f537bd4
keywords:
- KSPROPERTY_PIN_NAME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NAME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 640ef35b52fc0cff31c11d768e5631a61cb2f8ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380810"
---
# <a name="kspropertypinname"></a>KSPROPERTY\_PIN\_NAME


客户端使用 KSPROPERTY\_PIN\_要检索的 pin 工厂注册表名称的名称。 这是已本地化的 Unicode 字符串。

## <span id="ddk_ksproperty_pin_name_ks"></span><span id="DDK_KSPROPERTY_PIN_NAME_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p>包含已本地化的 Unicode 字符串的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定此属性使用 KSP\_PIN，其中该成员指定为其返回的注册表名称的 pin 工厂。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

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


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

 

 






