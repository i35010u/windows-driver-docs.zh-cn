---
title: WIA\_IPS\_条形码\_读取器
description: WIA\_IPS\_条形码\_WIA 微型驱动程序使用读取器属性来列出可用的条形码读取器位置 (/fixed 一个或多个) 和应用程序客户端，然后选择以下某个位置并启用条形码检测。
ms.assetid: EED6CE6D-38CC-4368-8722-5765849C5A7D
keywords:
- WIA_IPS_BARCODE_READER 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7756efebdc0cbb919d85c38649e38db087cd79b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569333"
---
# <a name="wiaipsbarcodereader"></a>WIA\_IPS\_条形码\_读取器


**WIA\_IPS\_条形码\_读取器**WIA 微型驱动程序使用属性来列出可用的条形码读取器位置 (/fixed 一个或多个) 和应用程序客户端，若要选择其中一个这些位置和启用条形码检测。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了所需的值**WIA\_IPS\_条形码\_读取器**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_READER_DISABLED</p></td>
<td><p>条形码检测已禁用。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_AUTO</p></td>
<td><p>条形码检测已启用。 条形码读取器位置是在具体取决于 active 扫描输入源的运行时自动选中的设备。</p></td>
</tr>
</tbody>
</table>

 

下表描述的可选值**WIA\_IPS\_条形码\_读取器**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_READER_FLATBED</p></td>
<td><p>条形码检测可用于扫描在扫描程序平台的文档。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_FRONT</p></td>
<td><p>条形码检测可用于在扫描程序送纸器上扫描的文档的正面。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_READER_FEEDER_BACK</p></td>
<td><p>条形码检测可用于在扫描程序送纸器上扫描的文档的正面。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_DUPLEX</p></td>
<td><p>条形码检测已启用。 条形码读取器位置是在具体取决于 active 扫描输入源的运行时自动选中的设备。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  WIA 微型驱动程序可以接受可选值的属性配置，但在扫描时忽略请求，以使条形码检测到的非活动状态的扫描输入源。

 

此属性是必需的所有条码读取器项。 WIA\_条形码\_读取器\_DISABLED 和 WIA\_条形码\_读取器\_自动值是必需的。 WIA\_条形码\_读取器\_禁用是所需的默认值。

[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性也是必需的所有条码读取器项。

下表描述了所需的值[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性实现条码读取器项上时。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaImgFmt_XmlBar</p></td>
<td><p>条形码元数据传输的内容是符合 WIA 条形码元数据架构的 XML 文件中。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</p></td>
<td><p>条形码元数据为 WIA 条形码元数据的原始格式的文件传输。</p></td>
</tr>
</tbody>
</table>

 

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





