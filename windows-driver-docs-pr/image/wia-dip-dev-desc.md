---
title: WIA \_ DIP \_ 开发 \_ DESC
description: WIA \_ DIP \_ DEV \_ DESC 属性包含 wia 微型驱动程序的设备描述字符串。 WIA 服务创建并维护此属性。
keywords:
- WIA_DIP_DEV_DESC 图像设备
topic_type:
- apiref
api_name:
- WIA_DIP_DEV_DESC
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce9f11e2c2cb9ecbd247e25e47c4c1d52a194a7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824521"
---
# <a name="wia_dip_dev_desc"></a>WIA \_ DIP \_ 开发 \_ DESC


WIA \_ DIP \_ DEV \_ DESC 属性包含 wia 微型驱动程序的设备描述字符串。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_dev_desc_si"></span><span id="DDK_WIA_DIP_DEV_DESC_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA \_ DIP \_ DEV DESC 属性包含的设备说明字符串 \_ 是从驱动程序的 INF 文件中获取的。 应用程序读取此属性以获取设备的说明。

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

 

 





