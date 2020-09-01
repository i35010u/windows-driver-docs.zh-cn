---
title: 步骤3设备的驱动程序已安装
description: 步骤3设备的驱动程序已安装
ms.assetid: 292c5ffe-fbdf-42b8-9642-024c78709843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e105b648edf6f213210e60a29d435d20b227b0b5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096215"
---
# <a name="step-3-the-driver-for-the-device-is-installed"></a>步骤 3:安装设备的驱动程序


在 Windows 为新设备选择最佳驱动程序后，它将通过以下方式保存有关设备和驱动程序的信息：

-   可以将相同型号和版本的多个设备连接到计算机。 每个设备连接称为 *设备实例*。

    Windows 将每个设备实例表示为唯一的设备节点 (*devnode*) 。 Devnode 包含设备的相关信息，例如设备是否已启动以及哪些驱动程序已在设备上注册了通知。

-   Windows 将设备的驱动程序表示为 *驱动程序节点*。 驱动程序节点基于[驱动程序包](driver-packages.md) [inf 文件](overview-of-inf-files.md)的 " [**INF*模型*" 部分**](inf-models-section.md)中匹配设备项的信息。 驱动程序节点包括设备的所有软件支持，如任何服务、设备特定的共同安装程序和注册表项。

一旦设备和驱动程序实例化，Windows 就会按以下步骤安装驱动程序：

1.  根据 [驱动程序包](driver-packages.md) [INF 文件](overview-of-inf-files.md)中的指令，Windows 执行以下操作：

    -   将驱动程序二进制文件和其他关联文件复制到由 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)指定的硬盘上的位置。

    -   执行任何与设备实例相关的配置，例如注册表项写入。

2.  Windows 从[驱动程序包的](driver-packages.md) [inf 文件](overview-of-inf-files.md)的 " [**INF 版本" 部分**](inf-version-section.md)中的**类**和**ClassGuid**项确定[设备安装程序类](./overview-of-device-setup-classes.md)。 若要优化设备安装，以相同方式设置和配置的设备将分为相同的设备安装程序类。

3.  复制驱动程序文件后，Windows 会立即将控制转移到 [即插即用 (PnP) manager](pnp-manager.md)。 PnP 管理器加载驱动程序并启动设备。

4.  PnP 管理器为设备加载适当的函数驱动程序和任何可选的筛选器驱动程序。

    PnP 管理器为尚未加载的任何必需的驱动程序调用 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 然后，PnP 管理器为每个驱动程序调用 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程，从较低的筛选器驱动程序开始，然后是函数驱动程序，最后是任何上层筛选器驱动程序。 PnP 管理器会根据需要将资源分配给设备，并将 [**IRP_MN_START_DEVICE**](../kernel/irp-mn-start-device.md) 发送到设备的驱动程序。

完成此步骤后，将立即安装并准备好使用设备。

 

