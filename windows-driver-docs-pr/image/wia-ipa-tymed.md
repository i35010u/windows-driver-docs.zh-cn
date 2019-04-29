---
title: WIA\_IPA\_TYMED
description: WIA\_IPA\_TYMED 属性包含图像传输的方法设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 3490f4b8-a1ed-4ab3-b621-ed87ce8ae9ea
keywords:
- WIA_IPA_TYMED 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_TYMED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55aa275754a5fad95cb53828f8b8080438096255
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365968"
---
# <a name="wiaipatymed"></a>WIA\_IPA\_TYMED


WIA\_IPA\_TYMED 属性包含图像传输的方法设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_tymed_si"></span><span id="DDK_WIA_IPA_TYMED_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_TYMED 属性来确定的数据传输的微型驱动程序的方法。

下表描述了有效使用 WIA 的常量\_IPA\_TYMED。

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
<td><p>TYMED_CALLBACK</p></td>
<td><p>将映像传输到内存中带区。</p>
<p>此常量是适用于 Windows Vista 和更高版本的操作系统已过时。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_FILE</p></td>
<td><p>将映像传输到一个文件。</p></td>
</tr>
<tr class="odd">
<td><p>TYMED_MULTIPAGE_CALLBACK</p></td>
<td><p>将多个映像传输到内存中带区。</p>
<p>此常量是适用于 Windows Vista 和更高版本的操作系统已过时。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_MULTIPAGE_FILE</p></td>
<td><p>将多个映像传输到一个文件。</p></td>
</tr>
</tbody>
</table>

 

所有 WIA 2.0 微型驱动程序必须将此属性的初始值都设置为其默认值，即 TYMED\_文件。

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

 

 





