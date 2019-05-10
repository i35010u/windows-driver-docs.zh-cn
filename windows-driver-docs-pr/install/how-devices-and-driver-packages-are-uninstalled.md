---
title: 如何卸载设备和驱动程序包
description: 如何卸载设备和驱动程序包
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a634c3d6d47ca5a66da123bc38b606c15f0ae8
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65456429"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>如何卸载设备和驱动程序包


本部分概述的需要执行的操作卸载设备和[驱动程序包](driver-packages.md)。 通过运行以下项之一来执行以下操作：

-   [设备管理器](using-device-manager.md)。

-   调用的设备安装应用程序[SetupAPI](setupapi.md)并[设备安装](https://msdn.microsoft.com/library/windows/hardware/ff541299)函数。

这些操作包括以下各项：

-   [卸载设备](#uninstalling-the-device)

-   [从驱动程序存储区中删除驱动程序包](#deleting-a-driver-package-from-the-driver-store)

-   [删除已安装的驱动程序的二进制文件](#deleting-the-binary-files-of-the-installed-driver)

**请注意**  无需按顺序执行这些操作。

 

### <a href="" id="uninstalling-the-device"></a> 卸载设备

这会卸载操作会删除设备节点 (*devnode*)，表示系统中的设备的物理实例。 使用以下方法之一删除 Devnodes:

-   设备管理器。 有关详细信息，请参阅[使用设备管理器](using-device-manager.md)。

-   调用的设备安装应用程序[SetupAPI](setupapi.md) [**SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)函数中的请求[ **DIF_删除**](https://msdn.microsoft.com/library/windows/hardware/ff543717)。 有关详细信息，请参阅[使用常规安装函数](using-general-setup-functions.md)。

-   设备安装应用程序调用 SetupAPI [ **DiUninstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544754)函数 （Windows 7 和更高版本的 Windows）。 有关详细信息，请参阅[使用设备安装函数](using-device-installation-functions.md)。

通过使用下列方法之一卸载设备后，请插即用 (PnP) 管理器中删除设备安装过程中创建的系统状态的子集。 例如，它将删除驱动程序二进制文件和设备之间的关联。 此关联用于通过服务控制管理器 (SCM) 加载适用于设备的驱动程序。

这会卸载操作不会撤消在安装过程中执行的所有操作。 例如，驱动程序包或*共同安装程序*（以及其他一些注册表操作） 将不会更改。

**请注意**  这卸载操作后完成后，devnode 设备不再存在，但是，对于[驱动程序包](driver-packages.md)仍然存在[驱动程序存储区](driver-store.md)。 如果 PnP 管理器重新枚举设备 （如当设备已断开，并再次接通），即插即用管理器将其视为新的设备实例，并从驱动程序存储区安装驱动程序包。

 

### <a href="" id="deleting-a-driver-package-from-the-driver-store"></a> 从驱动程序存储区中删除驱动程序包

这会卸载与相关联的文件操作删除[驱动程序包](driver-packages.md)从[驱动程序存储区](driver-store.md)和从 PnP 管理器的内部数据库中删除关联的元数据。 此操作还会删除[INF 文件](overview-of-inf-files.md)，这是与该驱动程序包，从系统 INF 目录相关联。

已从驱动程序存储区中删除驱动程序包后，就不再可用于在设备上安装。 必须重新加载并安装到驱动程序包[驱动程序存储区](driver-store.md)从原始源，例如光学媒体、 网络共享或 Windows 更新。

在删除之前的驱动程序包从驱动程序存储区，请务必卸载正在使用它的所有设备。

**重要**  您必须手动删除[驱动程序包](driver-packages.md)从[驱动程序存储区](driver-store.md)。 这样做可能会导致不一致造成 INF 文件、 驱动程序存储区目录中和驱动程序存储区中的驱动程序。 您可能还无法暂存驱动程序存储区的同一个驱动程序包。

 

### <a href="" id="deleting-the-binary-files-of-the-installed-driver"></a> 删除已安装的驱动程序的二进制文件

[设备管理器](using-device-manager.md)和 PnP 管理器不支持删除驱动程序二进制文件从安装位置的目标。 

当你卸载驱动程序包后时，仍可能由设备或应用程序中使用关联驱动程序二进制文件。 删除二进制文件可能会导致系统故障。 删除任何驱动程序的二进制文件之前，请确保二进制文件不是在系统上的任何其他组件仍在使用，可以安全地删除。



 

 





