---
title: IEEE 1394 驱动程序堆栈
description: IEEE 1394 驱动程序堆栈
ms.assetid: 3c8c218e-d814-451c-9a39-fe7fe5fb7aaf
keywords:
- IEEE 1394 WDK 总线，驱动程序堆栈
- 1394 WDK 总线，驱动程序堆栈
- 驱动程序堆栈 WDK IEEE 1394 总线
- 堆栈 WDK IEEE 1394 总线
- 设备堆栈 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b550fd58d087ffd5d6fef79dac14e77e5df7d65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841525"
---
# <a name="the-ieee-1394-driver-stack"></a>IEEE 1394 驱动程序堆栈





下图说明了 IEEE 1394 驱动程序堆栈，其中包含新的1394总线驱动程序和 Microsoft 支持的1394客户端驱动程序。

![说明 ieee 1394 驱动程序堆栈的关系图](images/1394driverstack.png)

连接到 IEEE 1394 总线驱动程序的设备的客户端驱动程序位于 IEEE 1394 驱动程序堆栈顶部。 总线驱动程序为 IEEE 1394 总线提供与硬件无关的接口。 设备驱动程序通过发送 Irp （由 IEEE 1394 总线驱动程序处理）与设备进行通信。 在 Windows 7 之前，总线驱动程序是端口驱动程序（1394bus）与主板的主机控制器（ochi1394）的主要微型端口驱动程序的组合。 在 Windows 7 及更高版本中，旧版端口/微型端口总线驱动程序由1394ohci （一个使用内核模式驱动程序框架（KMDF）实现的单一 IEEE 1394 总线驱动程序）替代。 1394ohci 总线驱动程序完全向后兼容旧的1394总线驱动程序。 有关新的总线驱动程序和旧式1394总线驱动程序之间行为的一些已知差异的详细信息，请参阅[Windows 7 中的 IEEE 1394 总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)。

下图显示了旧的和新的1394总线驱动程序之间的关系。

![显示旧的和新的1394总线驱动程序之间的关系的关系图。](images/1394busdriver.png)

为了向连接到总线的设备发出命令，驱动程序会向[**irp\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)IRP，并将控制代码[**IOCTL\_1394\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ni-1394-ioctl_1394_class)中。 驱动程序将参数打包到 IEEE 1394 i/o 请求块（[**IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb)）中，并将其指针传递到 IRP 的**Argument1**成员。 IRB 的**FunctionNumber**成员确定操作类型，而**u**成员描述操作。 总线驱动程序使用 IOCTL\_1394\_类 IRP 为总线和主机控制器提供一个接口。

IRB 结构包含适用于每个总线请求和请求特定参数的参数。 IRB 的**u**成员包含特定于请求的参数，在数据结构的联合中，每个请求类型一个。

在正常操作过程中，驱动程序将接收普通 i/o 请求（如[**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)），将其转换为相应的 IEEE 1394 操作，并通过 IOCTL\_1394\_类将该操作调度到设备。

## <a name="related-topics"></a>相关主题
[Windows 7 中的 IEEE 1394 总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  



