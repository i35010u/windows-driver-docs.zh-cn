---
title: 如何卸载设备和驱动程序包
description: 如何卸载设备和驱动程序包
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 10/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: aec0e880b371039d47c51e3dfaea6ff77999bb33
ms.sourcegitcommit: 735fea11056fe943c4368ee54573790e0602de66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91979984"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>如何卸载设备和驱动程序包

本页介绍了驱动程序如何卸载设备并从 [驱动程序存储区](driver-store.md)中删除驱动程序包。

## <a name="uninstalling-the-device"></a>卸载设备

若要删除设备节点 (表示物理设备的 *devnode*) ，请使用以下操作之一：

* 一种设备安装应用程序，它使用[**DIF_REMOVE**](./dif-remove.md)的请求来调用[setupapi.log](setupapi.md) [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller)函数。 有关详细信息，请参阅 [使用常规安装函数](using-general-setup-functions.md)。

* 调用 [**DiUninstallDevice**](/windows/win32/api/newdev/nf-newdev-diuninstalldevice) 函数的设备安装应用程序。 有关详细信息，请参阅 [使用设备安装功能](using-device-installation-functions.md)。

使用其中一种方法卸载设备时，即插即用 (PnP) manager 将删除驱动程序二进制文件与设备之间的关联。

设备仍保留在内核 PnP 树中， [驱动程序包](driver-packages.md) 保留在 [驱动程序存储区](driver-store.md)中。 如果 PnP 管理器重新枚举设备 (例如，如果设备已拔出，然后再次插入) ，则 PnP 管理器会将其视为新的设备实例，并从驱动程序存储区中安装驱动程序包。

有关最终用户如何卸载设备的信息，请参阅  [使用设备管理器卸载设备和驱动程序包](using-device-manager-to-uninstall-devices-and-driver-packages.md)。

## <a name="deleting-a-driver-package-from-the-driver-store"></a>从驱动程序存储区中删除驱动程序包

在从驱动程序存储区中删除驱动程序包之前，请确保卸载使用它的所有设备。

若要从[驱动程序存储区](driver-store.md)中删除[驱动程序包](driver-packages.md)，请使用以下选项之一：

* `pnputil /delete-driver <blah.inf> /uninstall`
* 使用 DevCon [按设备实例 ID 模式删除设备](../devtest/devcon-examples.md#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

从[驱动程序存储区](driver-store.md)中删除[驱动程序包](driver-packages.md)将从 PnP 管理器的内部数据库中删除关联的元数据，并从系统 INF 目录中删除相关的 INF 文件。

从驱动程序存储区中删除驱动程序包后，将无法再将其安装在设备上。 若要重新安装，请从原始源中再次下载驱动程序，如 Windows 更新。

从[驱动程序存储区](driver-store.md)中手动删除[驱动程序包](driver-packages.md)可能会导致不可预知的行为。

