---
title: DEVPKEY_DeviceClass_DHPRebalanceOptOut
description: 设备属性表示一个值，指示是否在资源重新平衡后的动态硬件分区 (DHP) 处理器热添加操作将参与整个设备类 DEVPKEY_DeviceClass_DHPRebalanceOptOut 发生。属性数据类型的 keyDEVPKEY_DeviceClass_DHPRebalanceOptOutProperty identifierDEVPROP_TYPE_BOOLEANProperty accessRead 和应用程序和服务的写访问权限。本地化的否 RemarksOn 正在运行 Windows Server 2008 或更高版本的 Windows Server，则操作系统将启动系统范围资源重新平衡新处理器动态添加到系统时的动态可分区服务器。 设备类参与 DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性不存在以下情况下重新平衡资源。设备属性存在并且未设置设备属性的值。设备属性存在，并且设备属性的值设置为 FALSE。如果存在 DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性和属性的值设置为 TRUE，设备类不参与新处理器动态添加到系统时，重新平衡资源。在设备的 INF 文件 INF 版本部分中指定设备的设备安装程序类。此属性 (Net 类) 的网络适配器的默认值为 TRUE。 此属性对于所有其他设备安装程序类的默认值为 FALSE。此设备属性不会影响是否设备类参与出于其他原因启动资源重新平衡。可以通过调用 SetupDiGetClassProperty 和 SetupDiSetClassProperty 访问 DEVPKEY_DeviceClass_DHPRebalanceOptOut 属性。
ms.assetid: e620ef24-b65d-4cf6-a21d-ffecad5804b4
keywords:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 96a6572278b9d63ff88dd81fdc43cbf350127962
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569035"
---
# <a name="devpkeydeviceclassdhprebalanceoptout"></a>DEVPKEY_DeviceClass_DHPRebalanceOptOut


DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性表示一个值，指示整个设备类将参与资源后重新平衡[动态硬件分区 (DHP)](https://msdn.microsoft.com/library/windows/hardware/ff544234)处理器热添加发生操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_DHPRebalanceOptOut</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入应用程序和服务的访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

**注释**

正在运行 Windows Server 2008 或更高版本的 Windows Server，则操作系统将启动系统范围资源的动态可分区服务器上重新平衡新处理器动态添加到系统时。 设备类参与资源重新平衡在以下情况下：

-   DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性不存在。

-   设备属性存在并且未设置设备属性的值。

-   设备属性存在且设备属性的值设置为**FALSE**。

如果存在 DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性和属性的值设置为 **，则返回 TRUE**，设备类不参与重新平衡时的新处理器动态添加到的资源系统。

设备的[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)中指定[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)的设备的 INF 文件。

网络适配器的此属性的默认值 (类 = Net) 是 **，则返回 TRUE**。 此属性对于所有其他设备安装程序类的默认值是**FALSE**。

此设备属性不会影响是否设备类参与出于其他原因启动资源重新平衡。

可以通过调用访问 DEVPKEY_DeviceClass_DHPRebalanceOptOut 属性[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)并[ **SetupDiSetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552128).

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
<td align="left"><p>在 Windows Server 2008 和更高版本的 Windows Server 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiSetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552128)

 

 






