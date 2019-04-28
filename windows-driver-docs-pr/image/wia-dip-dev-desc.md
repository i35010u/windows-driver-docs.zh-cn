---
title: WIA\_DIP\_开发人员\_DESC
description: WIA\_DIP\_开发人员\_DESC 属性包含用于 WIA 微型驱动程序的设备描述字符串。 WIA 服务创建并维护此属性。
ms.assetid: ce10deb8-7f33-45da-8a0e-cdcd7bf08ff9
keywords:
- WIA_DIP_DEV_DESC 成像设备
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
ms.openlocfilehash: 71886dc4750c1abc612f0046cfa5b21c6fe3e871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340139"
---
# <a name="wiadipdevdesc"></a>WIA\_DIP\_开发人员\_DESC


WIA\_DIP\_开发人员\_DESC 属性包含用于 WIA 微型驱动程序的设备描述字符串。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_dev_desc_si"></span><span id="DDK_WIA_DIP_DEV_DESC_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

设备描述字符串 WIA\_DIP\_开发人员\_DESC 属性包含从驱动程序的 INF 文件中获取。 应用程序读取此属性以获取设备的说明。

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

 

 





