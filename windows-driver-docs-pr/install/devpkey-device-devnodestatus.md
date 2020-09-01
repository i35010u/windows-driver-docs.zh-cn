---
title: DEVPKEY_Device_DevNodeStatus
description: DEVPKEY_Device_DevNodeStatus
ms.assetid: 538a78f0-c704-444e-8314-38b2e0421c39
keywords:
- DEVPKEY_Device_DevNodeStatus 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DevNodeStatus
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e3a499af5526fd6efc2d114822ff5966130cfde6
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096957"
---
# <a name="devpkey_device_devnodestatus"></a>DEVPKEY_Device_DevNodeStatus


DEVPKEY_Device_DevNodeStatus 设备属性表示设备节点 (*devnode*) 的状态。

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
<td align="left"><p>DEVPKEY_Device_DevNodeStatus</p></td>
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

DEVPKEY_Device_DevNodeStatus 的值是在 Cfg 中定义的 DN_*Xxx* 位标志的按位 "或"。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_DevNodeStatus 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何访问这些早期版本的 Windows 上的设备实例的状态的信息，请参阅 [检索设备实例的状态和问题代码](./retrieving-the-status-and-problem-code-for-a-device-instance.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**CM_Get_DevNode_Status**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

