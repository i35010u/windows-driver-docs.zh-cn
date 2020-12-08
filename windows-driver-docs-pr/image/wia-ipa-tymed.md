---
title: WIA \_ IPA \_ TYMED
description: WIA \_ IPA \_ TYMED 属性包含图像传输的方法设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_TYMED 图像设备
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
ms.openlocfilehash: e9dc64beccfb518398bc668150281ab0279afce1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796169"
---
# <a name="wia_ipa_tymed"></a>WIA \_ IPA \_ TYMED


WIA \_ IPA \_ TYMED 属性包含图像传输的方法设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_tymed_si"></span><span id="DDK_WIA_IPA_TYMED_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ TYMED 属性，以确定微型驱动程序的数据传输方法。

下表介绍了 WIA IPA TYMED 的有效常量 \_ \_ 。

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
<td><p>TYMED_CALLBACK</p></td>
<td><p>以带区传输图像到内存。</p>
<p>对于 Windows Vista 和更高版本的操作系统，此常量已过时。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_FILE</p></td>
<td><p>将图像传输到文件。</p></td>
</tr>
<tr class="odd">
<td><p>TYMED_MULTIPAGE_CALLBACK</p></td>
<td><p>以带区传输多个图像到内存。</p>
<p>对于 Windows Vista 和更高版本的操作系统，此常量已过时。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_MULTIPAGE_FILE</p></td>
<td><p>将多个图像传输到一个文件中。</p></td>
</tr>
</tbody>
</table>

 

所有 WIA 2.0 微型驱动程序都必须将此属性的初始值设置为其默认值（即 TYMED \_ 文件）。

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

 

 





