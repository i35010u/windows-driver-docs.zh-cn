---
title: 如何卸载设备和驱动程序包
description: 如何卸载设备和驱动程序包
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4512c45a1a4d82ecbe9ce17d4a93014e92090619
ms.sourcegitcommit: 4058fcb136cfb8255ca7bec68e8597c89f7b68cd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80080162"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>如何卸载设备和驱动程序包


本部分概述了卸载设备和[驱动程序包](driver-packages.md)所需执行的操作。 通过运行以下操作之一执行这些操作：

-   [设备管理器](using-device-manager.md)。

-   调用[setupapi.log](setupapi.md)和[设备安装](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))功能的设备安装应用程序。

这些操作包括以下各项：

-   [卸载设备](#uninstalling-the-device)

-   [从驱动程序存储区中删除驱动程序包](#deleting-a-driver-package-from-the-driver-store)

-   [正在删除已安装驱动程序的二进制文件](#deleting-the-binary-files-of-the-installed-driver)

**请注意**  这些操作不需要按顺序执行。

 

### <a name="uninstalling-the-device"></a><a href="" id="uninstalling-the-device"></a>卸载设备

此卸载操作将删除表示系统中设备的物理实例的设备节点（*devnode*）。 使用以下方法之一删除 Devnodes：

-   设备管理器。 有关详细信息，请参阅[使用设备管理器](using-device-manager.md)。

-   一种设备安装应用程序，它使用[**DIF_REMOVE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)的请求来调用[setupapi.log](setupapi.md) [**SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)函数。 有关详细信息，请参阅[使用常规安装函数](using-general-setup-functions.md)。

-   调用 Setupapi.log [**DiUninstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldevice)函数（windows 7 及更高版本的 windows）的设备安装应用程序。 有关详细信息，请参阅[使用设备安装功能](using-device-installation-functions.md)。

使用其中一种方法卸载设备时，即插即用（PnP）管理器会删除在设备安装过程中创建的系统状态的子集。 例如，它删除驱动程序二进制文件与设备之间的关联。 服务控制管理器（SCM）使用此关联加载设备的相应驱动程序。

此卸载操作不会撤消安装过程中执行的所有操作。 例如，驱动程序包或*共同安装*程序（与其他一些注册表操作一起）不会更改。

**请注意**  在此卸载操作完成后，设备的 devnode 将不再存在，但是[驱动程序包](driver-packages.md)仍存在于[驱动程序存储区](driver-store.md)中。 如果 PnP 管理器重新枚举设备（例如，拔出设备后再重新插入），PnP 管理器会将其视为新的设备实例，并从驱动程序存储区中安装驱动程序包。

 

### <a name="deleting-a-driver-package-from-the-driver-store"></a><a href="" id="deleting-a-driver-package-from-the-driver-store"></a>从驱动程序存储区中删除驱动程序包

此卸载操作从[驱动程序存储区](driver-store.md)中删除与[驱动程序包](driver-packages.md)关联的文件，并从 PnP 管理器的内部数据库中删除关联的元数据。 此操作还将从系统 INF 目录中删除与驱动程序包关联的[INF 文件](overview-of-inf-files.md)。

从驱动程序存储区中删除驱动程序包后，将无法再将其安装在设备上。 驱动程序包必须从原始源预留并安装到[驱动程序存储区](driver-store.md)中，如光学媒体、网络共享或 Windows 更新。

在从驱动程序存储区中删除驱动程序包之前，请确保卸载使用它的所有设备。

**重要**  您不得从[驱动程序存储区](driver-store.md)中手动删除[驱动程序包](driver-packages.md)。 这样做可能会导致 INF 文件、驱动程序存储目录和驱动程序存储区中的驱动程序不一致。 你可能还无法将同一驱动程序包暂存到驱动程序存储区。

 


 

 





