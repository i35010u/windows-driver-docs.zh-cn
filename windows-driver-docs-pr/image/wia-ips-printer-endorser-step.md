---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 步骤
description: 默认情况下，会在扫描的每个文档页上使用 imprinter/endorser imprints 或予以认可。
keywords:
- WIA_IPS_PRINTER_ENDORSER_STEP 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_STEP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3f434dccaf1236399e14b2d01ee1d1b10218133
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815107"
---
# <a name="wia_ips_printer_endorser_step"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 步骤


默认情况下，会在扫描的每个文档页上使用 imprinter/endorser imprints 或予以认可。 客户端可以使用 **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ STEP** 属性更改此强制的默认行为。 例如，客户端应用程序可以将当前值设置为2，以将每个其他扫描的页 imprinted/认可 (0，2，4，6，... ) 。WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ STEP** 属性的必需默认值为 1 () 每个页面。 值0无效。

对于大多数 WIA \_ \_ 属性范围属性，WIA 微型驱动程序可以实现一个范围，该范围包含一个单个值，最小等于最大值，步长值为零。

此属性必须受所有 Imprinter/Endorser 数据源项支持。 值 1 (需要) 每个页面。

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

 

 





