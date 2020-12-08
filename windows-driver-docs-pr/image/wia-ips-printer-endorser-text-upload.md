---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 文本 \_ 上传
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ TEXT \_ 上传属性用于报告 Imprinter/ENDORSER 项是否支持上传文本数据传输。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_TEXT_UPLOAD 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_TEXT_UPLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 521d8518a9774dc721377a08d5cef5921d3bb82b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815083"
---
# <a name="wia_ips_printer_endorser_text_upload"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 文本 \_ 上传


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ TEXT \_ 上传** 属性用于报告 Imprinter/ENDORSER 项是否支持上传文本数据传输。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4 (布尔) 

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为 True (非零) 值，则 WIA 微型驱动程序支持接收由应用程序客户端上载的文本数据。 传输文件格式由在同一 Imprinter/Endorser 项上实现的 [**wia \_ IPA \_ 格式**](wia-ipa-format.md) 和 [**wia \_ IPA \_ TYMED**](wia-ipa-tymed.md) 属性描述。

所有 Imprinter/Endorser 项都需要此属性，但可以实现此属性，以便始终报告值 0 (False) 。 此外，如果 Imprinter/Endorser 项报告 WiaItemTypeFile 和 WiaItemTypeTransfer，则此属性是必需的，并且必须报告非零值 (True) 。

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

 

 





