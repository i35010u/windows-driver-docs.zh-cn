---
title: WIA\_IPS\_打印机\_印记签署器\_文本\_下载
description: WIA\_IPS\_打印机\_印记签署器\_文本\_下载属性用于报告是否印刷器/印记签署器项支持下载文本数据传输。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: AEFF6C6F-8DA9-4AFF-8614-A1134C7C499C
keywords:
- WIA_IPS_PRINTER_ENDORSER_TEXT_DOWNLOAD 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_TEXT_DOWNLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6438233e31552ef13b1118a2972c30e276eb36e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351098"
---
# <a name="wiaipsprinterendorsertextdownload"></a>WIA\_IPS\_打印机\_印记签署器\_文本\_下载


WIA\_IPS\_打印机\_印记签署器\_文本\_下载属性用于报告是否印刷器/印记签署器项支持下载文本数据传输。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4 （布尔值）

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为值为 True （非零），WIA 微型驱动程序支持接收应用程序客户端上载的文本数据。 传输文件格式所描述[ **WIA\_IPA\_格式**](wia-ipa-format.md)并[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)实现相同的印刷器/印记签署器项上的属性。

此属性是必需的所有印刷器/印记签署器项，但它可以实现以始终报告的值为 0 (False)。

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

 

 





