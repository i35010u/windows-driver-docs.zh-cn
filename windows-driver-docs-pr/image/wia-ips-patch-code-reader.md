---
title: WIA \_ IPS \_ 修补程序 \_ 代码 \_ 读取器
description: WIA \_ IPS \_ 修补程序 \_ 代码 \_ 读取器属性用于启用修补程序代码检测。 所有修补程序代码读取器项都需要此属性。
keywords:
- WIA_IPS_PATCH_CODE_READER 图像设备
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
ms.openlocfilehash: 9a3c767e332618700a850a25720fe8abcad8984a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819507"
---
# <a name="wia_ips_patch_code_reader"></a>WIA \_ IPS \_ 修补程序 \_ 代码 \_ 读取器


**WIA \_ IPS \_ 修补程序 \_ 代码 \_ 读取器** 属性用于启用修补程序代码检测。 所有修补程序代码读取器项都需要此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 **WIA \_ IPS \_ 修补程序 \_ 代码 \_ 读取器** 属性的必需值。

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
<td><p>修补程序代码检测已禁用。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_READER_AUTO</p></td>
<td><p>修补程序代码检测已启用。 在运行时，设备会根据活动扫描输入源自动选择修补程序代码读取器位置。</p></td>
</tr>
</tbody>
</table>

 

所有修补程序代码读取器项还需要 [**WIA \_ IPA \_ 格式**](wia-ipa-format.md) 属性。

下表描述了在修补程序代码读取器项上实现 [**WIA \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性时该属性所需的值。

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
<td><p>修补程序代码元数据将传输为其内容符合 WIA 修补程序代码元数据架构的 XML 文件。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</p></td>
<td><p>修补程序代码元数据作为 WIA 修补程序代码元数据原始格式文件传输。</p></td>
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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





