---
title: DEVPKEY_Device_ProblemCode
description: DEVPKEY_Device_ProblemCode
keywords:
- DEVPKEY_Device_ProblemCode 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ProblemCode
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 02/28/2020
ms.openlocfilehash: 0056e88ded56693538fc7785614fd563ee7145eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828681"
---
# <a name="devpkey_device_problemcode"></a>DEVPKEY_Device_ProblemCode


DEVPKEY_Device_ProblemCode 设备属性表示设备实例的问题代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ProblemCode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_ProblemCode 的值是在 Cfg 中定义的 CM_PROB_ *Xxx* 的问题代码之一。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_ProblemCode 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何访问这些早期版本的 Windows 上的设备实例的问题代码的信息，请参阅 [检索设备实例的状态和问题代码](./retrieving-the-status-and-problem-code-for-a-device-instance.md)。

有关查找设备管理器或内核调试器中的问题状态的信息，请参阅 [检索设备实例的状态和问题代码](retrieving-the-status-and-problem-code-for-a-device-instance.md)。

有关可帮助解决问题的其他信息，请参阅 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

