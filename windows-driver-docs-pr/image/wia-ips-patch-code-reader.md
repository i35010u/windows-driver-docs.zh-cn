---
title: WIA\_IPS\_修补\_代码\_读取器
description: WIA\_IPS\_修补\_代码\_使用读取器属性以启用修补程序代码检测。 此属性是必需的所有修补程序代码读取器项。
ms.assetid: 8F008388-9822-44DC-B022-0822A8204740
keywords:
- WIA_IPS_PATCH_CODE_READER 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4759ba33817370d270d27063daacb641c235c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554300"
---
# <a name="wiaipspatchcodereader"></a>WIA\_IPS\_修补\_代码\_读取器


**WIA\_IPS\_修补\_代码\_读取器**属性用于启用修补程序代码检测。 此属性是必需的所有修补程序代码读取器项。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了所需的值**WIA\_IPS\_修补\_代码\_读取器**属性。

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
<td><p>WIA_PATCH_CODE_READER_DISABLED</p></td>
<td><p>禁用修补程序代码检测。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_READER_AUTO</p></td>
<td><p>启用了修补程序代码检测。 由设备所带来的具体取决于 active 扫描输入源的运行时自动选择的修补程序代码读取器位置。</p></td>
</tr>
</tbody>
</table>

 

[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性也是必需的修补程序代码读取器的所有项。

下表描述了所需的值[ **WIA\_IPA\_格式**](wia-ipa-format.md)属性实现修补程序代码读取器项上时。

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
<td><p>WiaImgFmt_XmlPat</p></td>
<td><p>修补程序代码的元数据传输的内容是符合 WIA 修补程序代码的元数据架构的 XML 文件中。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</p></td>
<td><p>修补程序代码的元数据为 WIA 修补程序代码的元数据的原始格式的文件传输。</p></td>
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

 

 





