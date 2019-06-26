---
title: 在 UMDF 驱动程序中使用设备池
description: 在 UMDF 驱动程序中使用设备池
ms.assetid: EC36CB33-3877-445B-8AC6-1D41E6397FF9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5a6ec95511af4b74ce0ee4d6c444b22111691e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372272"
---
# <a name="using-device-pooling-in-umdf-drivers"></a>在 UMDF 驱动程序中使用设备池


## <a name="user-mode-driver-framework-umdf-versions-111-and-20"></a>用户模式驱动程序框架 (UMDF) 版本 1.11 和 2.0


如果您的用户模式驱动程序框架 (UMDF) 驱动程序使用版本 1.11 或 2.0 已构建并正在运行 Windows 8 或更高版本，框架将创建可以托管多个设备堆栈的 Wudfhost 的单个实例。 这一技术称为*设备池*。 设备池的主要好处是减少的内存占用具有多个 UMDF 设备的环境中。

如果共用的设备无法正常工作，框架将终止 Wudfhost 实例并尝试重新启动所有以前的池中的设备。 如果设备无法再次共用时，框架将创建针对设备的单独 Wudfhost 进程和尝试重新启动设备。

如果设备无法在单独的主机进程，框架将尝试重新启动它最多五次。 框架将重置设备错误计数为一个当自上次失败已过去 30 分钟。

如果重新启动系统，该框架 repools 除之外的单独进程中运行时失败的设备。

若要禁用特定设备的设备池，请使用**UmdfHostProcessSharing** WDF 特定指令*DDInstall* INF 部分。 璝惠**UmdfHostProcessSharing**，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

如果您的驱动程序使用[直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)，则必须设置**UmdfHostProcessSharing**到**ProcessSharingDisabled**。 否则您的驱动程序可能无法启动。 如果**WdfDeviceIoBufferedOrDirect**处于选中状态和共用该设备，该框架更改到的缓冲区的访问方法[缓冲 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)。 如果**WdfDeviceIoBufferedOrDirect**处于选中状态并且设备将不入池，该框架将更改直接 I/O 的缓冲区的访问方法。

若要选择缓冲区的访问方法，您的驱动程序必须调用[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)方法从其[ **IDriverEntry::OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数。 有关访问方法的信息，请参阅[UMDF-Based 驱动程序中访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)。

## <a name="umdf-versions-19-and-earlier"></a>UMDF 版本 1.9 及更早版本


如果您的驱动程序已使用 UMDF 1.9 或更早版本生成的框架将创建每个设备堆栈的主机进程 (Wudfhost) 的单独实例。

如果设备无法启动，框架将尝试重新启动它最多五次。 框架将重置设备错误计数为一个当自上次失败已过去 30 分钟。

在非池化环境中，如果多个设备堆栈共享相同的 UMDF 驱动程序：

-   在单独的 WudfHost 进程中加载每个设备堆栈。
-   框架将调用的驱动程序[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)并[ **IDriverEntry::OnDeinitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)一次为每个方法设备堆栈。
-   框架将调用的驱动程序[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)一次为每个设备堆栈的方法。 每个设备对象是单独的驱动程序对象与相关联。

在共用环境中，如果多个设备堆栈共享相同的用户模式驱动程序：

-   同一个 WudfHost 进程中加载每个设备堆栈。
-   框架将调用的驱动程序[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)并[ **IDriverEntry::OnDeinitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)方法一次。
-   框架将调用的驱动程序[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)一次为每个设备堆栈的方法。 每个设备对象是与相同的驱动程序对象相关联。

由于共用的配置中只有一个驱动程序对象，该驱动程序不得存储任何每个设备上下文全局变量或设备，如驱动程序回调对象之间共享的对象中。 相反，该驱动程序必须存储设备堆栈，如驱动程序的设备回调对象之间未共享的对象中的每个设备上下文。

 

 





