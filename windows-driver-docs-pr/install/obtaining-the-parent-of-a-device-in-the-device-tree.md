---
title: 在设备树中获取某个设备的父设备
description: 在设备树中获取某个设备的父设备
ms.assetid: 0ac1ccbb-c926-4d14-975e-127159309361
keywords:
- Setupapi.log 函数 WDK，确定父项
- 确定 WDK Setupapi.log 的父设备
- 设备父 WDK
- SP_DEVINFO_DATA
- 连接的上级 WDK 的序列
- 祖先 WDK
- 设备树 WDK 中的直接父项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 137d89b1cc9516c053de31e80e0bf5e2db608e87
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716174"
---
# <a name="obtaining-the-parent-of-a-device-in-the-device-tree"></a>在设备树中获取某个设备的父设备





本主题介绍如何在设备树中获取 **SP_DEVINFO_DATA**) 。

**在设备树中获取设备的直接父级的 SP_DEVINFO_DATA 结构**

1.  通过对设备调用[**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status) ，验证设备是否在[设备树](../kernel/device-tree.md)中有 devnode：
    -   如果设备具有 devnode，则该函数将返回 CR_SUCCESS。
    -   如果设备没有 devnode，则该函数将返回 CR_NO_SUCH_DEVINST。

2.  如果设备具有 devnode，请调用 [**CM_Get_Parent**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_parent) 以获取设备父设备的设备实例句柄。

     (如果设备没有 devnode，则 **CM_Get_Parent** 返回根设备) 的设备实例句柄。

3.  使用父设备的设备实例句柄，调用 [**CM_Get_Device_ID**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw) 获取父设备的设备实例 ID。

4.  使用父设备的设备实例 ID，调用 [**SetupDiOpenDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinfoa) 来获取父设备的 SP_DEVINFO_DATA 结构。

**在设备树中获取设备的祖先的连接序列的 SP_DEVINFO_DATA 结构**

-   从设备的直接父项开始，到给定的祖先结束后，重复调用 **CM_Get_Parent** ，直到获取了所有句柄。 对于 **CM_Get_Parent**的每个调用，提供从上一个调用获取的设备实例句柄。

-   对于获取的每个设备实例句柄，请先调用 **CM_Get_Device_ID** 获取设备实例 ID，然后调用 **SetupDiOpenDeviceInfo** 获取设备的 SP_DEVINFO_DATA 结构。

有关如何使用 nonpresent 设备的信息，请参阅 [确定 Nonpresent 设备的父级](determining-the-parent-of-a-nonpresent-device.md)。

 

