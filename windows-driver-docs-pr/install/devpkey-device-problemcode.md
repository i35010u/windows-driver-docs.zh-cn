---
title: DEVPKEY_Device_ProblemCode
description: DEVPKEY_Device_ProblemCode
ms.assetid: 545fb6f7-660e-4df8-80cd-48b36910a518
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
ms.openlocfilehash: 223d5e811b400f1aa0869a43a382c6f2101c39bb
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418466"
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
<th>属性</th>
<th>Value</th>
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

DEVPKEY_Device_ProblemCode 的值是在 Cfg 中定义的 CM_PROB_*Xxx*的问题代码之一。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_ProblemCode 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何访问这些早期版本的 Windows 上的设备实例的问题代码的信息，请参阅[检索设备实例的状态和问题代码](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)。

有关查找设备管理器或内核调试器中的问题状态的信息，请参阅[检索设备实例的状态和问题代码](retrieving-the-status-and-problem-code-for-a-device-instance.md)。

有关可帮助解决问题的其他信息，请参阅[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

 






