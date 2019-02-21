---
title: WIA\_DIP\_端口\_名称
description: WIA\_DIP\_端口\_NAME 属性包含由运行在设备的内核模式驱动程序分配的已安装的设备的端口名称。 WIA 服务创建并维护此属性。
ms.assetid: ccb5d335-de56-477f-909c-cb2e55a0889a
keywords:
- WIA_DIP_PORT_NAME 成像设备
topic_type:
- apiref
api_name:
- WIA_DIP_PORT_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 500763de2381c0723f8842ff7dbbba1623340373
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541545"
---
# <a name="wiadipportname"></a>WIA\_DIP\_端口\_名称


WIA\_DIP\_端口\_NAME 属性包含由运行在设备的内核模式驱动程序分配的已安装的设备的端口名称。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_port_name_si"></span><span id="DDK_WIA_DIP_PORT_NAME_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DIP\_端口\_名称属性确定端口的名称。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





