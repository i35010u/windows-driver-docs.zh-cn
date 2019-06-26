---
title: 确定设备是否已插入
description: 确定设备是否已插入
ms.assetid: 26dc3c2b-49a6-4bba-b86b-2c93a1914f87
keywords:
- 重新安装拔出的设备
- 拔出的设备重新安装 WDK
- 检查接通电源的设备
- 验证接通电源的设备
- 设备检查 WDK 中插入
- 确定接通电源设备 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 927cd785bb86c6a80f4d16209f2cc05d87f9ce63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358204"
---
# <a name="determining-whether-a-device-is-plugged-in"></a>确定设备是否已插入


请注意，自动运行调用的行为*设备安装应用程序*必须依赖于是否用户插入硬件中第一次或第一次插入分发介质。 由于独立硬件供应商 (Ihv) 通常会提供一个分发磁盘，并且磁盘只能有一个自动运行调用应用程序，因此将自动运行调用设备安装应用程序必须确定是否在插入你的设备。

若要确定是否在插入设备，应用程序可以调用[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)函数，传递的设备硬件 ID。 如果以下项之一为 true，将在插入设备：

-   该函数将返回 **，则返回 TRUE**。 （这也会安装该设备驱动程序。）

-   该函数将返回**FALSE**和 Win32 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)函数返回 ERROR_NO_MORE_ITEMS。 （没有安装出现。）

如果该函数将返回不在插入设备**FALSE**并[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)返回 NO_SUCH_DEVINST。 （没有安装出现。）

### <a name="reinstalling-an-unplugged-device"></a>重新安装拔出的设备

以前已附加的设备现已拔出，设备的*devnode*保持在系统中，尽管它是处于非活动状态和隐藏。 您可以重新安装此类设备之前，必须先找到此"虚拟"devnode，并将其标记为需要重新安装。 然后时返回在插入设备，, 插将 reenumerate 设备、 查找新的驱动程序，并安装设备驱动程序。

**若要重新安装拔出的设备：**

1.  调用[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=98735)函数。

    [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)函数还可确保正确的 INF 文件是否存在于 *%systemroot%\\inf*目录。

2.  查找拔出的设备。

    调用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)函数。 在对此函数调用中，清除中的 DIGCF_PRESENT 标志*标志*参数。 您需要找到*所有*设备，而不仅仅是那些存在。 可以通过指定中的特定设备类来缩小搜索结果范围*ClassGuid*参数。

3.  查找硬件 Id 和兼容拔出设备 Id。

    **SetupDiGetClassDevs**返回的句柄[设备的信息集](device-information-sets.md)是否已插入或中 （假定您在第一步中指定的设备类） 的设备类，包含所有已安装的设备。 通过连续调用来[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)函数，您可以使用此句柄以枚举设备的信息集中的所有设备。 每次调用为您提供了[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)设备的结构。 若要获取的硬件 Id 列表，请调用[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)函数与*属性*参数设置为 SPDRP_HARDWAREID。 若要获取的兼容 Id 列表，请调用相同的函数，但*属性*参数设置为 SPDRP_COMPATIBLEIDS。 这两个列表是多 SZ 的字符串。

4.  查找你的设备和硬件 Id （或兼容 Id） 的上一步骤的 ID 相匹配。

    请确保为你的设备执行之间的硬件 ID/兼容 ID 和 ID 的完整字符串比较。 部分比较可能会导致不正确的匹配项。

    当找到匹配项时，调用[ **CM_Get_DevNode_Status** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)函数，传递 SP_DRVINFO_DATA。**DevInst**中*dnDevInst*参数。 如果此函数返回 CR_NO_SUCH_DEVINST，来确认是否未附加设备 （即，具有虚拟 devnode）。

5.  将设备标记。

    调用[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)函数与*属性*参数设置为 SPDRP_CONFIGFLAGS。 此函数返回时， *PropertyBuffer*参数指向的设备**配置标志**注册表中的值。 执行与 CONFIGFLAG_REINSTALL 此值的按位或 (在中定义*Regstr.h*)。 在执行此操作之后, 调用[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)函数，使用*属性*参数设置为 SPDRP_CONFIGFLAGS，和*PropertyBuffer*参数设置为设备的地址的修改**配置标志**值此操作会修改注册表的**配置标志**值将合并CONFIGFLAG_REINSTALL 标志。 这将导致在重新安装下次重新枚举设备的设备。

6.  插入设备。

    插将 reenumerate 设备、 查找新的驱动程序，并安装该驱动程序。

 

 





