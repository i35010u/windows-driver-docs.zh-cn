---
title: 更新使用 Windows 更新设备固件
description: 本主题介绍如何使用 Windows Update (WU) 服务的设备的固件更新。
ms.assetid: 778c5ab5-572f-43b9-8e9a-9dd608de17a9
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6eeab3f3f202b34af9f094e2dd56380f3b9735b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523011"
---
# <a name="updating-device-firmware-using-windows-update"></a>更新使用 Windows 更新设备固件

本主题介绍如何使用 Windows Update (WU) 服务的可移动或机箱中设备的固件更新。  有关更新系统固件的信息，请参阅[Windows UEFI 固件更新平台](../bringup/windows-uefi-firmware-update-platform.md)。

若要执行此操作，将提供一个更新机制，实现为的设备驱动程序，包括固件有效负载。  如果你的设备使用供应商提供的驱动程序，必须将固件更新逻辑和有效负载添加到现有函数驱动程序，或提供单独的固件更新驱动程序包的选项。  如果你的设备使用 Microsoft 提供的驱动程序，则必须提供单独的固件更新驱动程序包。  在这两种情况下，必须是通用的固件更新驱动程序包。  有关通用驱动程序的详细信息，请参阅[通用 Windows 驱动程序入门](../develop/getting-started-with-universal-drivers.md)。  可以使用驱动程序二进制文件[KMDF](../wdf/index.md)， [UMDF 2](../wdf/getting-started-with-umdf-version-2.md)或[Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)。 

因为 WU 无法执行软件、 固件更新驱动程序必须分发固件插 (PnP) 安装。

## <a name="firmware-update-driver-actions"></a>固件更新驱动程序操作

通常情况下，固件更新驱动程序是轻量设备驱动程序，执行以下任务：

* 设备启动时或在驱动程序中[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数：

    1. 识别附加到的设备。
    2. 确定驱动程序是否在设备上的版本比新的固件版本。
    3. 如果固件更新是必需的设置事件计时器计划更新。
    4. 否则，执行任何操作之前重新启动该驱动程序。

* 在系统运行时：

    1. 如果更新已排队，等待要满足的条件集。
    2. 当满足条件时，请在设备上执行固件更新。

## <a name="firmware-update-driver-contents"></a>固件更新驱动程序内容

通常情况下，固件更新驱动程序包包含以下元素：

* [通用驱动程序 INF](using-a-universal-inf-file.md)
* 驱动程序目录
* 功能驱动程序 （.sys 或.dll）
* 固件更新负载二进制

将作为单独的驱动程序提交提交固件更新包。

## <a name="adding-firmware-update-logic-to-a-vendor-supplied-driver"></a>将固件更新逻辑添加到供应商提供的驱动程序

现有功能驱动程序可以实现固件更新机制，如以下关系图中所示：

![使用 Windows 更新将通过现有功能驱动程序的固件更新](images/single-devnode.png)

或者，如果你想要单独更新功能驱动程序和固件更新驱动程序，创建第二个设备节点中，将其安装固件更新驱动程序。  下图显示了如何一台设备可以有两个单独的设备节点：

![使用 Windows 更新将通过单独的设备节点的固件更新](images/two-devnodes.png)

在这种情况下，函数和固件设备节点必须具有不同的硬件 Id，才能为独立目标。

有几种方法来创建第二个设备节点。  特定设备类型可以公开一个物理设备，如 USB 上的第二个设备节点。  可以使用此功能将创建一个设备节点通过 WU，定目标，并在其上安装固件更新驱动程序。  但是，许多设备类型，不允许在单个物理设备来枚举多个设备节点。

在这种情况下，使用扩展指定的 INF [AddComponent](../install/inf-addcomponent-directive.md)指令以创建一个设备节点，可以通过 Windows 更新目标并在其上安装固件更新驱动程序。  INF 文件的以下代码段显示了如何执行此操作：

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

在上面的示例 INF 中，`ComponentIDs = ComponentDeviceId`指示子设备都将具有的硬件 ID `SWC\ComponentDeviceId`。  安装时，此 INF 创建以下设备层次结构：

![父设备、 主要设备、 AddComponent 的设备](images/component-device-hierarchy.png)

对于将来的固件更新，更新的 INF 和二进制文件包含固件负载。

## <a name="adding-firmware-update-logic-to-a-microsoft-supplied-driver"></a>向 Microsoft 提供的驱动程序添加固件更新逻辑

若要使用 Microsoft 提供的驱动程序的设备的固件更新，需要创建第二个设备节点中，如上所示。

## <a name="best-practices"></a>最佳做法

* 在您的固件更新驱动程序 INF 中，指定[DIRID 13](using-dirids.md)使即插即用来保留在 DriverStore 驱动程序包中的文件：

    ```cpp
    [Firmware_AddReg]
    ; Store location of firmware payload
    HKR,,FirmwareFilename,,"%13%\firmware_payload.bin"
    ```

    即插即用安装设备时解析此位置。  该驱动程序然后可以打开此注册表项来确定有效负载的位置。

* 固件更新驱动程序应指定以下 INF 条目：

    ```cpp
    Class=Firmware
    ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
    ```

* 若要查找设备的另一个节点，固件驱动程序应树设备相对于自身，不通过匹配枚举设备的所有节点。  用户可能已接通电源的设备，多个实例和固件驱动程序应只更新与之关联的设备。  通常情况下，要查找的设备节点为父级或在其安装固件驱动程序的设备节点的同级。 例如，在关系图中上方具有两个设备节点，固件更新驱动程序可以查找同级设备发现功能驱动程序。  立即上面的关系图中的固件驱动程序可以查找父设备发现它需要进行通信的主要设备。

* 该驱动程序应该能够正常处理到由可能具有多个不同的固件版本的系统上的设备的多个实例。  例如，可能有一个实例的设备的已连接并进行更新几次;全新的设备然后可能接通这是旧的多个固件版本。  这意味着对该设备，而不是在全局位置必须存储状态 （例如当前版本）。

* 如果没有现有方法更新固件 （EXE 或共同安装程序，例如），可以很大程度上重用内 UMDF 驱动程序的更新代码。
