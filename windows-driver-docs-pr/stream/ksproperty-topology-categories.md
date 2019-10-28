---
title: KSPROPERTY\_拓扑\_类别
description: KSPROPERTY\_拓扑\_类别 "属性查询驱动程序支持的功能类别的数组。
ms.assetid: 35a293a1-f8fe-44da-a50b-a4429e369567
keywords:
- KSPROPERTY_TOPOLOGY_CATEGORIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_CATEGORIES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d37380229e81651e903c7685beed1253bcdd3cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837930"
---
# <a name="ksproperty_topology_categories"></a>KSPROPERTY\_拓扑\_类别


KSPROPERTY\_拓扑\_类别 "属性查询驱动程序支持的功能类别的数组。

## <span id="ddk_ksproperty_topology_categories_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_CATEGORIES_KS"></span>


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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>，后跟一个 guid 序列</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构，后跟一系列 guid，表示 KS 筛选器支持的功能类别。 Microsoft 在*ks*和*ksmedia*中提供了标准类别。 下面列出了非特定于技术的功能类别：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能类别</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCATEGORY_BRIDGE</p></td>
<td><p>在内核流式处理子系统之外桥接。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_CAPTURE</p></td>
<td><p>This.</p></td>
</tr>
<tr class="odd">
<td><p></p>
KSCATEGORY_ COMMUNICATIONSTRANSFORM</td>
<td><p>通信转换设备。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATACOMPRESSOR</p></td>
<td><p>压缩数据流。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
<td><p>解压缩数据流。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATATRANSFORM</p></td>
<td><p>转换数据流。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_FILESYSTEM</p></td>
<td><p>将数据流移入或移出文件系统。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_INTERFACETRANSFORM</p></td>
<td><p>转换所使用的接口类型。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_MEDIUMTRANSFORM</p></td>
<td><p>转换正在使用的媒体类型。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_MIXER</p></td>
<td><p>混合多个数据流。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_RENDER</p></td>
<td><p>呈现.</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_SPLITTER</p></td>
<td><p>拆分数据流。</p></td>
</tr>
</tbody>
</table>

 

拓扑类别对应于设备接口类。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSTOPOLOGY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






