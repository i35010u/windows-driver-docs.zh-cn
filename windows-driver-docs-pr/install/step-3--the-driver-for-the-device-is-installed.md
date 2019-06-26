---
title: 步骤 3 的设备驱动程序安装
description: 步骤 3 的设备驱动程序安装
ms.assetid: 292c5ffe-fbdf-42b8-9642-024c78709843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8106f257165427ae1d7d57f70664465506b68c8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385875"
---
# <a name="step-3-the-driver-for-the-device-is-installed"></a>步骤 3:安装设备的驱动程序


Windows 已选择新设备的最佳驱动程序后，它将按以下方式保存的设备和驱动程序有关的信息：

-   相同的模型和版本的多个设备可以连接到计算机。 每个设备连接称为*设备实例*。

    Windows 表示为一个唯一的设备节点的每个设备实例 (*devnode*)。 Devnode 包含有关设备，例如设备是否已启动，以及哪些驱动程序已注册的设备上的通知的信息。

-   Windows 表示为设备的驱动程序*驱动程序节点*。 驱动程序节点基于从匹配的设备项中的信息[ **INF*模型*部分**](inf-models-section.md)的[驱动程序包的](driver-packages.md) [INF 文件](overview-of-inf-files.md)。 驱动程序节点包括的设备，如任何服务、 特定于设备的共同安装程序和注册表项的所有软件支持。

只要设备和驱动程序进行实例化，则 Windows 安装驱动程序通过执行以下步骤：

1.  根据中的指令[驱动程序包](driver-packages.md) [INF 文件](overview-of-inf-files.md)，Windows 将执行以下操作：

    -   驱动程序二进制文件以及其他关联的文件复制到指定的硬盘上的位置的副本[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

    -   执行任何设备实例相关的配置，如写入注册表项。

2.  Windows 确定[设备安装程序类](device-setup-classes.md)从**类**并**ClassGuid**中的条目[ **INF 版本部分**](inf-version-section.md)的[驱动程序包](driver-packages.md) [INF 文件](overview-of-inf-files.md)。 若要优化设备安装，设备设置和配置相同的方式被分组到同一设备安装程序类。

3.  只要将驱动程序文件复制，Windows 将控制转移到[插即用 (PnP) 管理器](pnp-manager.md)。 PnP 管理器加载的驱动程序，并使设备开始。

4.  PnP 管理器将加载相应的功能驱动程序和设备的任何可选的筛选器驱动程序。

    PnP 管理器调用[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程尚未加载任何所需驱动程序。 PnP 管理器然后调用[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程的较低的筛选器驱动程序，从开始，每个驱动程序功能驱动程序，然后，最后，任何上部的筛选器驱动程序。 PnP 管理器将资源分配到设备，如有必要，并将发送[**执行了 IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)到设备的驱动程序。

一旦完成此步骤后，设备已安装并可供使用。

 

 





