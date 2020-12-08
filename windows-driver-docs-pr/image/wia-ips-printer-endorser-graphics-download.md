---
title: WIA \_ IP \_ 打印机 \_ ENDORSER \_ 图形 \_ 下载
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS \_ 下载属性用于报告 Imprinter/ENDORSER 项是否支持下载图像 (图形) 数据传输。 此属性由 WIA 微型驱动程序初始化和维护。
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_DOWNLOAD 图像设备
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
ms.openlocfilehash: c8faeebffb33fe4bb92f9c63de5ff014f8e2076f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839083"
---
# <a name="wia_ips_printer_endorser_graphics_download"></a>WIA \_ IP \_ 打印机 \_ ENDORSER \_ 图形 \_ 下载


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ GRAPHICS \_ 下载** 属性用于报告 Imprinter/ENDORSER 项是否支持下载图像 (图形) 数据传输。 此属性由 WIA 微型驱动程序初始化和维护。




属性类型： VT \_ I4 (布尔) 

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果将此属性的当前值设置为非零值 (True) ，则意味着 WIA 微型驱动程序支持通过 WIA 应用程序客户端传输下载的图像数据。 传输文件格式由在同一 Imprinter/Endorser 项上实现的 [**wia \_ IPA \_ 格式**](wia-ipa-format.md) 和 [**wia \_ IPA \_ TYMED**](wia-ipa-tymed.md) 属性描述。

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

 

 





