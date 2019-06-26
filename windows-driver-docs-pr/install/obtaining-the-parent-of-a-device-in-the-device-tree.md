---
title: 在设备树中获取某个设备的父设备
description: 在设备树中获取某个设备的父设备
ms.assetid: 0ac1ccbb-c926-4d14-975e-127159309361
keywords:
- 安装程序 Api 函数 WDK，确定父项
- 父设备确定 WDK SetupAPI
- 设备父级 WDK
- SP_DEVINFO_DATA
- 连接的序列的上级 WDK
- 上级 WDK
- 在设备树 WDK 的直接父项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc93f63c6fcab85a2b3a645a266746370eb9ad6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366668"
---
# <a name="obtaining-the-parent-of-a-device-in-the-device-tree"></a>在设备树中获取某个设备的父设备





本主题介绍如何获取**SP_DEVINFO_DATA**) 设备树中。

**若要获取设备树中的设备的直接父级 SP_DEVINFO_DATA 结构**

1.  验证设备中有 devnode[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)通过调用[ **CM_Get_DevNode_Status** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)设备：
    -   如果该设备已 devnode，该函数将返回 CR_SUCCESS。
    -   如果设备不具有 devnode，该函数将返回 CR_NO_SUCH_DEVINST。

2.  如果该设备已 devnode，调用[ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)父级的设备获取设备实例句柄。

    (如果设备不具有 devnode **CM_Get_Parent**返回根设备的设备实例句柄)。

3.  父设备使用设备实例句柄，调用[ **CM_Get_Device_ID** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)来获取父设备的设备实例 ID。

4.  父设备使用设备实例 ID，调用[ **SetupDiOpenDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)获取父设备 SP_DEVINFO_DATA 结构。

**若要获取的祖先构成设备树中的设备的连接序列的 SP_DEVINFO_DATA 结构**

-   设备的直接父级开头和结尾给定祖先，请调用**CM_Get_Parent**重复之前获取的所有句柄。 每次调用**CM_Get_Parent**，供应设备实例句柄来自前面的调用。

-   为你获取每个设备实例句柄，第一次调用**CM_Get_Device_ID**若要获取设备实例 ID，然后调用**SetupDiOpenDeviceInfo**若要获取的 SP_DEVINFO_DATA 结构设备。

有关如何使用虚幻设备的信息，请参阅[确定的父级的 Nonpresent 设备](determining-the-parent-of-a-nonpresent-device.md)。

 

 





