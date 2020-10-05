---
title: 确定设备是否已插入
description: 确定设备是否已插入
ms.assetid: 26dc3c2b-49a6-4bba-b86b-2c93a1914f87
keywords:
- 重新安装拔出的设备
- 拔下设备重新安装 WDK
- 检查接通电源的设备
- 验证接通电源的设备
- 插入设备检查 WDK
- 确定是否已接通设备 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 542245d83d4893dce3005e6bd97289e9940420a7
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733181"
---
# <a name="determining-whether-a-device-is-plugged-in"></a>确定设备是否已插入


请注意，自动运行调用的 *设备安装应用程序* 的行为必须取决于用户是要插入到硬件中还是首先插入分布介质。 由于独立硬件供应商 (Ihv) 通常提供一个分发磁盘，而一个磁盘只能有一个自动运行调用的应用程序，所以，自动运行的设备安装应用程序必须确定设备是否已插入。

若要确定设备是否已插入，应用程序可以调用 [**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa) 函数，同时传递设备的硬件 ID。 如果满足以下任一条件，则会插入设备：

-   该函数返回 **TRUE**。  (这还会安装设备的驱动程序。 ) 

-   该函数返回 **FALSE** ，Win32 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)函数返回 ERROR_NO_MORE_ITEMS。  (不会进行安装。 ) 

如果此函数返回 **FALSE** ，且 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 返回 NO_SUCH_DEVINST，则不插入设备。  (不会进行安装。 ) 

### <a name="reinstalling-an-unplugged-device"></a>重新安装拔出的设备

现在已拔下先前附加的设备时，设备的 *devnode* 将保留在系统中，但它既处于非活动状态又处于隐藏状态。 在重新安装此类设备之前，必须先找到此 "虚拟" devnode，并将其标记为需要重新安装。 然后，在设备重新插回时，即插即用将 reenumerate 设备，查找新的驱动程序，并为设备安装驱动程序。

**重新安装拔出的设备：**

1.  调用 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa) 函数。

    [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa)函数可确保 *% SystemRoot% \\ INF*目录中存在正确的 INF 文件。

2.  找到拔出的设备。

    调用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 函数。 在对此函数的调用中，清除 *Flags* 参数中的 DIGCF_PRESENT 标志。 你必须查找 *所有* 设备，而不只是显示那些设备。 可以通过在 *ClassGuid* 参数中指定特定设备类来缩小搜索结果的范围。

3.  查找设备的硬件 Id 和兼容 Id。

    如果设备类 (假设你在第一) 步中指定了设备类，则**SetupDiGetClassDevs**将返回设备[信息集](device-information-sets.md)的句柄，其中包含已安装的所有设备（无论是否插入）。 通过对 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 函数进行连续调用，你可以使用此句柄枚举设备信息集中的所有设备。 每次调用都提供设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。 若要获取硬件 Id 列表，请调用 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 函数，并将 *属性* 参数设置为 SPDRP_HARDWAREID。 若要获取兼容 Id 的列表，请调用相同的函数，但将 *属性* 参数设置为 SPDRP_COMPATIBLEIDS。 这两个列表都是多 SZ 字符串。

4.  查找你的设备 ID 与上一步的硬件 id (或兼容 Id) 之间的匹配。

    请确保对设备的硬件 ID/兼容 ID 与 ID 执行完整的字符串比较。 部分比较可能导致不正确的匹配项。

    找到匹配项后，调用[**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)函数，同时传递 SP_DRVINFO_DATA。*DnDevInst*参数中的**DevInst** 。 如果此函数返回 CR_NO_SUCH_DEVINST，则该函数将确定设备是否为未附加 (，即具有一个虚拟 devnode) 。

5.  将设备标记为。

    调用 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 函数，并将 *属性* 参数设置为 SPDRP_CONFIGFLAGS。 此函数返回时， *PropertyBuffer* 参数将从注册表指向设备的 **ConfigFlags** 值。 使用 *Regstr*) 中定义的 CONFIGFLAG_REINSTALL (来执行此值的按位 or。 完成此操作后，调用 [**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) 函数，将 *Property* 参数设置为 SPDRP_CONFIGFLAGS，并将 *PropertyBuffer* 参数设置为设备的已修改 **CONFIGFLAGS** 值的地址。此操作会修改注册表的 **CONFIGFLAGS** 值以合并 CONFIGFLAG_REINSTALL 标志。 这会导致在下次设备 reenumerated 时重新安装该设备。

6.  插入设备。

    即插即用将 reenumerate 设备，查找新的驱动程序，并安装该驱动程序。

