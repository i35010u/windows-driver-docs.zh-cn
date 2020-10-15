---
title: 如何卸载设备和驱动程序包
description: 如何卸载设备和驱动程序包
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 10/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: a08e736b294285d228780add21515abf8b2e1e61
ms.sourcegitcommit: f001f5163e1f6350cc8b6dffcc078733defcd053
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92061737"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>如何卸载设备和驱动程序包

本页说明软件如何卸载设备并从 [驱动程序存储区](driver-store.md)中删除驱动程序包。

## <a name="uninstalling-the-device"></a>卸载设备

若要删除设备节点 (表示物理设备的 *devnode*) ，请使用以下操作之一：

* 若要仅卸载指定的设备，请使用设备安装应用程序，该应用程序使用 DIF_REMOVE 的请求来调用[setupapi.log](setupapi.md)   函数[**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 。 [**DIF_REMOVE**](./dif-remove.md)

* 若要在设备树中卸载指定设备及其下面的任何设备，请使用调用 [**DiUninstallDevice**](/windows/win32/api/newdev/nf-newdev-diuninstalldevice) 函数的设备安装应用程序。

使用其中一种方法卸载设备时，即插即用 (PnP) manager 将删除驱动程序二进制文件与设备之间的关联。

设备仍保留在内核 PnP 树中， [驱动程序包](driver-packages.md) 保留在 [驱动程序存储区](driver-store.md)中。 如果 PnP 管理器重新枚举设备 (例如，如果设备已拔出，然后再次插入) ，则 PnP 管理器会将其视为新的设备实例，并从驱动程序存储区中安装驱动程序包。

有关最终用户如何卸载设备的信息，请参阅  [使用设备管理器卸载设备和驱动程序包](using-device-manager-to-uninstall-devices-and-driver-packages.md)。

## <a name="deleting-a-driver-package-from-the-driver-store"></a>从驱动程序存储区中删除驱动程序包

若要从[驱动程序存储区](driver-store.md)中删除[驱动程序包](driver-packages.md)，请执行以下操作之一：

* 在命令提示符下，使用 `pnputil /delete-driver <example.inf> /uninstall` 。 有关 PnPUtil 命令的信息，请参阅 [PnPUtil 命令语法](../devtest/pnputil-command-syntax.md)。
* 在 Windows 10 版本1703或更高版本上，设备安装应用程序可以调用 [**DiUninstallDriverW**](/windows/win32/api/newdev/nf-newdev-diuninstalldriverw)。
* 在早期版本的 Windows 上，设备安装应用程序应该首先发出 [**DIF_REMOVE**](./dif-remove.md) 请求，或调用 [**DiUninstallDevice**](/windows/win32/api/newdev/nf-newdev-diuninstalldevice) 函数来卸载所有设备，然后调用 [**SetupUninstallOEMInf**](/windows/win32/api/setupapi/nf-setupapi-setupuninstalloeminfa) 以删除驱动程序。

从驱动程序存储区中删除驱动程序包将从 PnP 管理器的内部数据库中删除关联的元数据，并从系统 INF 目录中删除相关的 INF 文件。

删除驱动程序包后，它将无法再安装在设备上。 若要重新安装，请从原始源中再次下载驱动程序，如 Windows 更新。

从[驱动程序存储区](driver-store.md)中手动删除[驱动程序包](driver-packages.md)可能会导致不可预知的行为。
