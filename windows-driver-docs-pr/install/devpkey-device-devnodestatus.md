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
ms.openlocfilehash: 9237670b04b259027cf898ba11f21478f555233b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546627"
---
# <a name="devpkeydevicedevnodestatus"></a>DEVPKEY_Device_DevNodeStatus


DEVPKEY_Device_DevNodeStatus 设备属性表示设备节点的状态 (*devnode*)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DevNodeStatus 的值是 DN_ 的按位 OR*Xxx*位 Cfg.h 中定义的标志。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_DevNodeStatus 值。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持此属性。 有关如何访问这些早期版本的 Windows 上的设备实例的状态信息，请参阅[检索的设备实例的状态和问题代码](https://msdn.microsoft.com/library/windows/hardware/ff550651)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CM_Get_DevNode_Status**](https://msdn.microsoft.com/library/windows/hardware/ff538514)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






