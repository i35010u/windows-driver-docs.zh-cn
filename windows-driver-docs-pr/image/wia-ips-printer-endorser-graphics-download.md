---
title: WIA\_IPS\_打印机\_印记签署器\_图形\_下载
description: WIA\_IPS\_打印机\_印记签署器\_图形\_下载属性用于报告是否印刷器/印记签署器项支持下载映像 （图形） 数据传输。 此属性是初始化和维护的 WIA 微型驱动程序。
ms.assetid: AE58548B-CB0A-45FE-A1C6-5C476061B89D
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_DOWNLOAD 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_DOWNLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bedbdc2d186a4352c7aaa19bbc29861fbf38220
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566724"
---
# <a name="wiaipsprinterendorsergraphicsdownload"></a>WIA\_IPS\_打印机\_印记签署器\_图形\_下载


**WIA\_IPS\_打印机\_印记签署器\_图形\_下载**属性用于报告的印刷器/印记签署器项是否支持下载图像 （图形） 数据传输。 此属性是初始化和维护的 WIA 微型驱动程序。




属性类型：VT\_I4 （布尔值）

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为非零值 (True)，这意味着 WIA 微型驱动程序支持 WIA 应用程序客户端下载到它的图像数据传输。 传输文件格式所描述[ **WIA\_IPA\_格式**](wia-ipa-format.md)并[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)实现相同的印刷器/印记签署器项上的属性。

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

 

 





