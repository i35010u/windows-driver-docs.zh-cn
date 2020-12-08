---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 文本 \_ 下载
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ TEXT \_ 下载属性用于报告 Imprinter/ENDORSER 项是否支持下载文本数据传输。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_TEXT_DOWNLOAD 图像设备
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
ms.openlocfilehash: 6e51c8cb159b581862e5d85099686fd2c7b0912d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815095"
---
# <a name="wia_ips_printer_endorser_text_download"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 文本 \_ 下载


WIA \_ IPS \_ PRINTER \_ ENDORSER \_ TEXT \_ 下载属性用于报告 Imprinter/ENDORSER 项是否支持下载文本数据传输。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4 (布尔) 

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果此属性的当前值设置为 True (非零) 值，则 WIA 微型驱动程序支持接收由应用程序客户端上载的文本数据。 传输文件格式由在同一 Imprinter/Endorser 项上实现的 [**wia \_ IPA \_ 格式**](wia-ipa-format.md) 和 [**wia \_ IPA \_ TYMED**](wia-ipa-tymed.md) 属性描述。

此属性对所有 Imprinter/Endorser 项是必需的，但它可以实现为始终报告值 0 (False) 。

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

 

 





