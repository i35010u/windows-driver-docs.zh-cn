---
title: WIA\_IPS\_MICR\_READER
description: WIA 微型驱动程序使用 WIA\_IPS\_MICR\_读取器属性来报告可用磁性墨迹字符识别 (MICR) 读取器位置。 WIA 客户端应用程序可以选择在其中启用 MICR 检测这些位置之一。
ms.assetid: 093A5EDF-BFD6-42BD-B532-9CB578EA284C
keywords:
- WIA_IPS_MICR_READER 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MICR_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c84bcf1512604082fecdbfcdd381c0da7553488b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520241"
---
# <a name="wiaipsmicrreader"></a>WIA\_IPS\_MICR\_READER


使用 WIA 微型驱动程序**WIA\_IPS\_MICR\_读取器**属性来报告可用磁性墨迹字符识别 (MICR) 读取器位置。 WIA 客户端应用程序可以选择在其中启用 MICR 检测这些位置之一。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了所需的值**WIA\_IPS\_MICR\_读取器**属性。

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
<td><p>WIA_MICR_READER_DISABLED</p></td>
<td><p>禁用 MICR 检测。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_AUTO</p></td>
<td><p>启用 MICR 检测。 MICR 读取器位置固定的或在运行时根据 active 扫描输入源设备自动选择。</p></td>
</tr>
</tbody>
</table>

 

此属性是必需的所有 MICR 读取器项。 WIA\_MICR\_读取器\_DISABLED 和 WIA\_MICR\_读取器\_自动值是必需的。 WIA\_MICR\_读取器\_禁用是所需的默认值。

下表描述的可选值**WIA\_IPS\_MICR\_读取器**属性。

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
<td><p>WIA_MICR_READER_FLATBED</p></td>
<td><p>在平台扫描的文档启用 MICR 检测。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_FRONT</p></td>
<td><p>MICR 检测可用于通过送纸器已扫描文档的正面。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MICR_READER_FEEDER_BACK</p></td>
<td><p>MICR 检测可用于通过送纸器已扫描文档的正面。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_DUPLEX</p></td>
<td><p>为这两个前端启用 MICR 检测和送纸器通过扫描文档的后端。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  WIA 微型驱动程序可以接受可选值的属性配置，但在扫描时忽略请求，以使 MICR 检测到的非活动状态的扫描输入源。

 

[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性也是必需的 MICR 读取器的所有项。

下表描述了所需的值[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性实现 MICR 读取器项上时。

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
<td><p>WiaImgFmt_XmlMic</p></td>
<td><p>MICR 元数据将传输的内容是符合 WIA MICR 元数据架构的 XML 文件。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawMic</p></td>
<td><p>为 WIA MICR 元数据的原始格式的文件传输 MICR 元数据。</p></td>
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
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





