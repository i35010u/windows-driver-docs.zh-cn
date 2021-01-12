---
title: 确定设备的父设备
description: 确定设备的父设备
keywords:
- Setupapi.log 函数 WDK，确定父项
- 确定 WDK Setupapi.log 的父设备
- 设备父 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf71be53eea9238eb856c52b73587ee8953ca398
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124215"
---
# <a name="determining-the-parent-of-a-device"></a>确定设备的父设备





有时需要访问设备的父级。 例如，某些类型的硬件设备的操作取决于特定父设备与子设备集之间的固定关系。 若要卸载此类硬件设备，你必须卸载除所有子设备之外的父项。 若要卸载父级，必须获取父对象的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。 通用串行总线 (USB) 复合设备（如多功能打印机）是这样一种设备。 它在系统中由父复合设备和一个或多个子接口设备表示 (参阅 [USB 驱动程序堆栈体系结构](../usbcon/usb-3-0-driver-stack-architecture.md)) 。 若要卸载多功能打印机，你必须卸载其父复合设备及其所有子接口设备。

当 [即插即用](../kernel/introduction-to-plug-and-play.md) (PnP) manager 在系统中配置设备时，会将设备 (*devnode*) 添加到 [设备树](../kernel/device-tree.md)中。 当 PnP 管理器从系统中删除设备时，它将从设备树中删除设备的 devnode，设备将成为 *nonpresent 设备*。 确定设备父项所用的方法取决于当前在系统中配置设备的方式，如下所示：

-   如果设备在设备树中具有 devnode，请使用 [**CM_Get_Parent**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_parent) 获取其父对象的设备实例句柄。 给定设备实例句柄，可以获取设备的 [设备实例 ID](device-instance-ids.md) 和 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。 有关详细信息，请参阅 [在设备树中获取设备的父级](obtaining-the-parent-of-a-device-in-the-device-tree.md)。

-   如果设备具有与其父级的固定关系，则可以保存并检索其父项的设备实例 ID。 当设备变为 nonpresent 时，可以使用其设备实例句柄获取设备的 SP_DEVINFO_DATA 结构。 有关详细信息，请参阅 [确定 Nonpresent 设备的父级](determining-the-parent-of-a-nonpresent-device.md)。