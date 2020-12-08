---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形 \_ 上传
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS \_ 上传属性用于报告 Imprinter/ENDORSER 项是否支持) 数据传输上传 (图形的图像。 此属性由 WIA 微型驱动程序初始化和维护。
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_UPLOAD 图像设备
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
ms.openlocfilehash: 88bbb1c2f2eea95dc8c482c05ca3eefe50ad2881
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798163"
---
# <a name="wia_ips_printer_endorser_graphics_upload"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形 \_ 上传


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS \_ 上传** 属性用于报告 Imprinter/ENDORSER 项是否支持) 数据传输上传 (图形的图像。 此属性由 WIA 微型驱动程序初始化和维护。




属性类型： VT \_ I4 (布尔) 

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为非零值 (True) ，则表示 WIA 微型驱动程序支持接收由 WIA 应用程序客户端上载到的图像数据。 传输文件格式由在同一 Imprinter/Endorser 项上实现的 [**wia \_ IPA \_ 格式**](wia-ipa-format.md) 和 [**wia \_ IPA \_ TYMED**](wia-ipa-tymed.md) 属性描述。

此属性是必需的，并且对报告非零值 (True) 用于 [**WIA \_ IPS \_ 打印机 \_ Endorser \_ 图形**](wia-ips-printer-endorser-graphics.md)的所有 Imprinter/Endorser 项是必需的，但它可以实现为始终报告0值 (False) 。 否则，属性无效。

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

 

 





