---
title: 对 ACPI 服务使用 PEP
description: 本主题提供有关使用 ACPI 服务平台扩展插件 (Pep) 的信息。
ms.assetid: 80ED3B80-A1FF-4A41-BA88-EC1C832C4639
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 907c720c1541ae9a256ec9da2051fad972c91ae3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381584"
---
# <a name="using-peps-for-acpi-services"></a>对 ACPI 服务使用 PEP


本主题提供有关使用 ACPI 服务平台扩展插件 (Pep) 的信息。

Pep 提供动态，运行时 ACPI 方法。 必须在 ACPI 固件，以及 DSDT/SSDT 设备层次结构中实现静态表 （FADT、 MADT、 DBG2 等）。

Pep 旨在用于关闭 SoC 电源管理方法。 因为它们是可安装二进制文件，它们可以是更新上动态而不是 ACPI 固件这要求刷新固件。 这意味着您可以提高您已交付在 Windows 更新上发布更新的驱动程序的平台上应用电源管理代码。 电源管理的原始意图的 Pep，但它们可以使用来提供或重写任何任意 ACPI 运行时方法。

因为命名空间层次结构必须提供在固件 DSDT Pep ACPI 命名空间层次结构的构造中不起任何作用。 当 ACPI 驱动程序的计算结果的方法在运行时，它将检查设备有问题，PEP 的实现方法，并且如果存在，它将执行 PEP 并忽略的固件版本。 但是，在设备本身必须定义在固件中。

提供电源管理使用 Pep 可以是更易于调试比 ACPI 固件由于提供的工具编写的代码。 适用于调试 ACPI 固件工具是最不熟悉和工具选项限制。 与此相反，Pep 会开发作为 Windows 驱动程序，因此开发人员可以使用任何开发和调试工具它们是最合适。

如果使用 PEP 来代替 ACPI 服务，任何特殊操作则需要以声明的服务的角色。 当方法在 PEP 中实现时，Windows 将自动使用。 如果提供的相同方法在同一设备上的固件版本，则它将被忽略。

以使其服务的设备驱动程序可用，很早加载 Pep。 此外，通过 Windows 的抽象层旨在对设备驱动程序是透明的。 该驱动程序应能够像 PEP 未在使用与它的 ACPI 方法进行交互。

使用 PEP 设备电源管理 (DPM) 和 ACPI 服务，它时，建议使用单独 PEP 句柄，但这只是一个首选项。 当共享 DPM 和 ACPI 状态的句柄可以跟踪轻松设备因为句柄都是相同。 但是，句柄生存期管理是稍微复杂一些。 PEP 将需要提供引用计数的句柄，以确保它仅删除后 DPM 和 ACPI 服务具有已销毁该句柄 (即，两者[ **PEP\_DPM\_注销\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并[ **PEP\_通知\_ACPI\_注销\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)已收到该句柄上）。 当使用不同的句柄时，将单独跟踪 DPM 和 ACPI 状态但句柄生存期管理更为简单。 在这种情况下，该句柄可被销毁时相应取消注册发送通知。

为了简化使用 ACPI 资源的过程，电源管理框架 (PoFx)，提供了 PEP\_请求\_常见\_ACPI\_转换\_TO\_BIOS\_资源的帮助器例程，以将 ACPI 资源转换为 BIOS 资源。

Pep 负责计划不能以响应来自 PoFx 的 ACPI 通知以同步方式执行工作，但使用的方法由 PEP 开发人员。 通常情况下，PEP 将队列上某些内部队列的工作，并根据需要启动工作线程。 此外，还可以工作，需要等待某些外部事件 （例如设备中断），会处理该事件的上下文中。 PEP 完成工作后，可以通过调用查询的工作请求 PoFx [ **PEP\_内核\_信息\_结构\_V3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/ns-pepfx-_pep_kernel_information_struct_v3) - &gt; [ *RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pofxcallbackrequestworker)（)。 在响应中，将发送 PoFx [ **PEP\_DPM\_工作通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)对于实现 DPM 通知处理程序的 Pep ([ *AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifydpm)) 或[ **PEP\_通知\_ACPI\_工作通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)为 PEPs实现仅限 ACPI 的通知处理程序 ([*AcceptAcpiNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifyacpi))。

## <a name="related-topics"></a>相关主题
[ACPI 系统说明表](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)  
[**PEP\_DPM\_UNREGISTER\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_NOTIFY\_ACPI\_UNREGISTER\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_内核\_信息\_结构\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)  
[**PEP\_DPM\_工作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_NOTIFY\_ACPI\_WORK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[*RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pofxcallbackrequestworker)  
[*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifydpm)  
[ACPI 通知](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  



