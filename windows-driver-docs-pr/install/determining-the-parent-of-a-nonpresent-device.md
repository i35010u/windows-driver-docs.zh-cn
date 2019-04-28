---
title: 确定虚幻设备的父设备
description: 确定虚幻设备的父设备
ms.assetid: 2d5948db-5844-4f78-b3a6-2f9f88ee1b24
keywords:
- 安装程序 Api 函数 WDK，确定父项
- 虚幻设备 WDK
- 父设备确定 WDK SetupAPI
- 设备父级 WDK
- 父-子关系 WDK
- 保存父-子关系
- 检索父-子关系
- 连接的序列的上级 WDK
- 上级 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c035b398accb563efca4635424e0e0f8f690aba1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346171"
---
# <a name="determining-the-parent-of-a-nonpresent-device"></a>确定虚幻设备的父设备





可以使用在本部分中介绍的方法来确定的父级*虚幻设备*才固定的虚幻设备及其父级之间的关系。 （如果不解决虚幻设备及其父级之间的关系，则你不能使用此方法，因为虚幻的设备不具有特定父）。

例如，此方法适用于 USB 复合设备，如的多功能打印机，有一个或多个接口，其中每个表示为子设备。 由于所有子接口设备都取决于作为其父级存在特定的复合设备，设备及其父级之间的关系被固定。

以下主题介绍了此方法：

[正在保存父/子关系](#saving-the-parent-child-relationship)

[检索父/子关系](#retrieving-the-parent-child-relationship)

[处理虚幻设备的上级链](#handling-a-chain-of-ancestors-for-a-nonpresent-device)

### <a href="" id="saving-the-parent-child-relationship"></a> 正在保存父/子关系

若要保存的设备的父/子关系，请提供*设备共同安装程序*，它将设备的父级的设备实例 ID 保存在设备的硬件注册表项下创建用户项值。 应使用设备实例 ID，因为它保持不变系统进程之间以及跨系统重新启动而没有设备实例句柄。 当处理[ **DIF_INSTALLDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff543692)请求共同安装程序中，执行以下步骤以保存设备实例 id。

***<em>若要在注册表中保存的直接父级的设备实例 ID</em>***

1.  调用[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)父级的设备获取设备实例句柄。

2.  父设备使用设备实例句柄，调用[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)来获取父设备的设备实例 ID。

3.  调用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)使用 DIREG_DEV 标志获取到设备的硬件注册表项句柄。

4.  调用**RegSetValueEx**将保存在设备的硬件注册表项下创建用户项值中的父设备的设备实例 ID。

### <a href="" id="retrieving-the-parent-child-relationship"></a> 检索父/子关系

设备共同安装程序在设备的硬件注册表项下的项值中保存了父设备的设备实例 ID 后，可以检索设备实例 id。

***<em>若要从注册表中检索的父级的设备实例 ID</em>***

1.  调用**SetupDiOpenDevRegKey** DIREG_DEV 标志用于获取设备的硬件注册表项的句柄。

2.  调用**RegQueryValueEx**检索保存在设备共同安装程序中设置的项值中的父设备的设备实例 ID。

检索父设备的设备实例 ID 后，调用[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)若要获取[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)父设备的结构。

### <a href="" id="handling-a-chain-of-ancestors-for-a-nonpresent-device"></a> 处理虚幻设备的上级链

如果为给定设备需要连接序列中的上级的设备实例 Id，应保存可以检索它们的方式在注册表中的每个祖先的设备实例 ID。 请注意，这是固定设备和所有祖先之间的关系时才有效。

这是用于设备共同安装程序，以使用一个方法可以解决**CM_Get_Parent**获取所有设备的所有祖先的实例 Id，并将每个实例 ID 保存在设备的硬件注册表项下的不同输入值。 可以使用中所述的方法[保存父/子关系](#saving-the-parent-child-relationship)以保存每个祖先的设备实例 ID。 然后可以检索每个设备实例 ID 相同的方式如中所述[检索父/子关系](#retrieving-the-parent-child-relationship)。

 

 





