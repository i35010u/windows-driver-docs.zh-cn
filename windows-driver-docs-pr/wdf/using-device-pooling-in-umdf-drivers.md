---
title: 在 UMDF 驱动程序中使用设备池
description: 在 UMDF 驱动程序中使用设备池
ms.assetid: EC36CB33-3877-445B-8AC6-1D41E6397FF9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 733197185e967f13821ce113115269a66297b861
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843087"
---
# <a name="using-device-pooling-in-umdf-drivers"></a>在 UMDF 驱动程序中使用设备池


## <a name="user-mode-driver-framework-umdf-versions-111-and-20"></a>用户模式驱动程序框架（UMDF）版本1.11 和2。0


如果你的用户模式驱动程序框架（UMDF）驱动程序是使用版本1.11 或2.0 生成的，并且在 Windows 8 或更高版本上运行，则该框架将创建可托管多个设备堆栈的单个 Wudfhost 实例。 此方法称为*设备池*。 设备池的主要优点是减少了具有多个 UMDF 设备的环境中的内存消耗。

如果共用设备出现故障，则该框架将终止 Wudfhost 实例，并尝试重新启动池中的所有设备。 如果在共用时设备再次失败，框架将为设备创建一个单独的 Wudfhost 进程，并再次尝试启动设备。

如果设备在单独的主机进程中出现故障，则该框架将尝试将其重启5次。 在上一次失败后，框架会将设备错误计数重置为1。

如果重新启动系统，框架 repools 设备除外，在单独的进程中运行时失败。

若要禁用特定设备的设备池，请使用 INF 中特定于 WDF 的*DDInstall*部分中的**UmdfHostProcessSharing**指令。 有关**UmdfHostProcessSharing**的信息，请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

如果驱动程序使用[直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)，则必须将**UmdfHostProcessSharing**设置为**ProcessSharingDisabled**。 否则，驱动程序可能无法启动。 如果选择了 " **WdfDeviceIoBufferedOrDirect** " 并将设备汇集到池中，则框架会将缓冲区访问方法更改为[缓冲 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)。 如果选择了 " **WdfDeviceIoBufferedOrDirect** " 且设备未建立池连接，框架会将缓冲区访问方法更改为直接 i/o。

若要选择缓冲区访问方法，驱动程序必须从其[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数调用[**IWDFDeviceInitialize2：： SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)方法。 有关访问方法的信息，请参阅[在基于 UMDF 的驱动程序中访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)。

## <a name="umdf-versions-19-and-earlier"></a>UMDF 版本1.9 及更早版本


如果驱动程序是使用 UMDF 1.9 版或更早版本生成的，则该框架将为每个设备堆栈创建一个单独的宿主进程（Wudfhost）的实例。

如果设备无法启动，则框架将尝试将其重新启动5次。 在上一次失败后，框架会将设备错误计数重置为1。

在非汇集环境中，如果多个设备堆栈共享同一 UMDF 驱动程序：

-   每个设备堆栈在单独的 WudfHost 进程中加载。
-   框架为每个设备堆栈调用驱动程序的[**IDriverEntry：： OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)和[**IDriverEntry：： OnDeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)方法一次。
-   框架为每个设备堆栈调用驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法一次。 每个设备对象与一个单独的驱动程序对象相关联。

在共用环境中，如果多个设备堆栈共享同一用户模式驱动程序：

-   每个设备堆栈在同一 WudfHost 进程中加载。
-   框架只调用驱动程序的[**IDriverEntry：： OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)和[**IDriverEntry：： OnDeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)方法一次。
-   框架为每个设备堆栈调用驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法一次。 每个设备对象与同一个驱动程序对象相关联。

由于在一个共用的配置中只有一个驱动程序对象，因此驱动程序不得在全局变量或在设备之间共享的对象（如驱动程序回调对象）中存储任何每个设备上下文。 相反，驱动程序必须将每个设备的上下文存储在不在设备堆栈之间共享的对象中，如驱动程序的设备回调对象。

 

 





