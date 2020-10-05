---
title: 使用 Windows 更新更新设备固件
description: 本主题介绍如何使用 Windows 更新 (WU) 服务来更新设备的固件。
ms.assetid: 778c5ab5-572f-43b9-8e9a-9dd608de17a9
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f9be0109536bcd0d6b2d7f744f26a405ecc3a1
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733677"
---
# <a name="updating-device-firmware-using-windows-update"></a>使用 Windows 更新更新设备固件

本主题介绍如何使用 Windows 更新 (WU) 服务来更新可移动或机箱设备的固件。  有关更新系统固件的信息，请参阅 [WINDOWS UEFI 固件更新平台](../bringup/windows-uefi-firmware-update-platform.md)。

为此，你将提供一个作为设备驱动程序实现的更新机制，其中包括固件负载。  如果设备使用供应商提供的驱动程序，则可以选择将固件更新逻辑和负载添加到现有的函数驱动程序，或者提供单独的固件更新驱动程序包。  如果设备使用 Microsoft 提供的驱动程序，则必须提供单独的固件更新驱动程序包。  在这两种情况下，固件更新驱动程序包必须是通用的。  有关通用驱动程序的详细信息，请参阅 [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)。  驱动程序二进制文件可以使用 [KMDF](../wdf/index.md)、 [UMDF 2](../wdf/getting-started-with-umdf-version-2.md) 或 [Windows 驱动模型](../kernel/writing-wdm-drivers.md)。 

由于 WU 无法执行软件，固件更新驱动程序必须将固件手动即插即用 (PnP) 安装。

## <a name="firmware-update-driver-actions"></a>固件更新驱动程序操作

通常，固件更新驱动程序是一种轻型设备驱动程序，它执行以下操作：

* 在设备启动或驱动程序的 [*EVT_WDF_DRIVER_DEVICE_ADD*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中：

    1. 确定要连接到的设备。
    2. 确定驱动程序的固件版本是否低于当前在设备硬件上闪存的固件版本。
    3. 如果需要固件更新，请设置事件计时器来计划更新。
    4. 否则，不执行任何操作，直到重新启动驱动程序。

* 在系统运行时：

    1. 如果更新已排队，请等待满足一组条件。
    2. 满足条件时，在设备上执行固件更新。

## <a name="firmware-update-driver-contents"></a>固件更新驱动程序内容

通常，固件更新驱动程序包包含以下各项：

* [通用驱动程序 INF](using-a-universal-inf-file.md)
* 驱动程序目录
* 函数驱动程序 ( .sys 或 .dll) 
* 固件更新负载二进制

提交固件更新包作为单独的驱动程序提交。

## <a name="adding-firmware-update-logic-to-a-vendor-supplied-driver"></a>将固件更新逻辑添加到供应商提供的驱动程序

现有函数驱动程序可以实现固件更新机制，如下图所示：

![使用 Windows 更新通过现有函数驱动程序传送固件更新](images/single-devnode.png)

或者，如果你要单独更新函数驱动程序和固件更新驱动程序，请创建另一个设备节点，你将在该节点上安装固件更新驱动程序。  下图显示了一个设备可以有两个单独的设备节点：

![使用 Windows 更新通过单独的设备节点交付固件更新](images/two-devnodes.png)

在这种情况下，函数和固件设备节点必须具有不同的硬件 Id 才能单独进行目标。

有几种方法可以创建第二个设备节点。  某些设备类型能够在一个物理设备（如 USB）上公开另一个设备节点。  你可以使用此功能创建不再的设备节点，并在其上安装固件更新驱动程序。  但许多设备类型不允许单个物理设备枚举多个设备节点。

在这种情况下，请使用指定 [AddComponent](../install/inf-addcomponent-directive.md) 指令的扩展 INF，以创建可 Windows 更新并在其上安装固件更新驱动程序的设备节点。  INF 文件中的以下代码片段显示了如何执行此操作：

```cpp
[Manufacturer]
%Contoso%=Standard,NTamd64
[Standard.NTamd64]
%DeviceName%=Device_Install, PCI\DEVICE_ID
[Device_Install.Components]
AddComponent=ComponentName,,AddComponentSection
[AddComponentSection]
ComponentIDs = ComponentDeviceId
```

在上述 INF 示例中， `ComponentIDs = ComponentDeviceId` 指示子设备将具有的硬件 ID `SWC\ComponentDeviceId` 。  安装此 INF 后，会创建以下设备层次结构：

![父设备，主设备，AddComponent 设备](images/component-device-hierarchy.png)

对于将来的固件更新，请更新包含固件有效负载的 INF 和二进制文件。

## <a name="adding-firmware-update-logic-to-a-microsoft-supplied-driver"></a>将固件更新逻辑添加到 Microsoft 提供的驱动程序

若要更新使用 Microsoft 提供的驱动程序的设备固件，需要创建另一个设备节点，如上所示。

## <a name="best-practices"></a>最佳做法

* 在固件更新驱动程序 INF 中，指定 [DIRID 13](using-dirids.md) 以使 PnP 将文件保留在 DriverStore 中的驱动程序包中：

    ```cpp
    [Firmware_AddReg]
    ; Store location of firmware payload
    HKR,,FirmwareFilename,,"%13%\firmware_payload.bin"
    ```

    PnP 在安装设备时解析此位置。  然后，驱动程序可以打开此注册表项以确定有效负载的位置。

* 固件更新驱动程序应指定以下 INF 条目：

    ```cpp
    Class=Firmware
    ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
    ```

* 若要查找另一个设备节点，固件驱动程序应使设备树相对于其自身，而不是枚举所有设备节点进行匹配。  用户可能已连接到设备的多个实例，并且固件驱动程序只应更新与其关联的设备。  通常，要定位的设备节点是安装固件驱动程序的设备节点的父节点或同级节点。 例如，在上面的关系图中，有两个设备节点，固件更新驱动程序可以查找同级设备以查找函数驱动程序。  在上面的关系图中，固件驱动程序可以查找父设备，查找需要与其通信的主要设备。

* 驱动程序在系统上的多个实例（可能有多个不同的固件版本）上应该是可靠的。  例如，可能有一个设备已连接并更新多次的实例;然后，可能会插入一台全新设备，其中有多个固件版本旧。  这意味着，必须将状态 (例如，当前版本) 必须存储在设备上，而不是存储在全局位置。

* 如果现有方法更新固件 (EXE 或共同安装程序，例如) ，则可以很大程度地重复使用 UMDF 驱动程序中的更新代码。