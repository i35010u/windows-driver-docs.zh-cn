---
title: WIA\_IPS\_打印机\_印记签署器\_图形\_上传
description: WIA\_IPS\_打印机\_印记签署器\_图形\_上传属性用于报告是否印刷器/印记签署器项支持上传映像 （图形） 数据传输。 此属性是初始化和维护的 WIA 微型驱动程序。
ms.assetid: BCA1F340-5BF8-429A-90B9-9638E52E61DE
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_UPLOAD 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_UPLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1271c01b4b643fcb128d8e834b1f19f36d86c89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352088"
---
# <a name="wiaipsprinterendorsergraphicsupload"></a>WIA\_IPS\_打印机\_印记签署器\_图形\_上传


**WIA\_IPS\_打印机\_印记签署器\_图形\_上载**属性用于报告的印刷器/印记签署器项是否支持上传映像 （图形）数据传输。 此属性是初始化和维护的 WIA 微型驱动程序。




属性类型：VT\_I4 （布尔值）

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为非零值 (True)，这意味着 WIA 微型驱动程序支持接收由 WIA 应用程序客户端上传到它的图像数据。 传输文件格式所描述[ **WIA\_IPA\_格式**](wia-ipa-format.md)并[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)实现相同的印刷器/印记签署器项上的属性。

此属性是必需的和有效的所有印刷器/印记签署器项的报告非零值 (True)，以便[ **WIA\_IPS\_打印机\_印记签署器\_图形**](wia-ips-printer-endorser-graphics.md)，但它可以实现对始终为 0 (False) 值的报表。 否则，该属性是无效。

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

 

 





