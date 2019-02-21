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
ms.openlocfilehash: 905dcdc0fc71127055ae60e6bf043fd7d3622ce2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526609"
---
# <a name="the-ieee-1394-driver-stack"></a>IEEE 1394 驱动程序堆栈





下图演示了使用新的 1394年总线驱动程序和支持 Microsoft 的 1394年客户端驱动程序的 IEEE 1394 驱动程序堆栈。

![说明 ieee 1394 驱动程序堆栈的关系图](images/1394driverstack.png)

用于连接到 IEEE 1394 总线驱动程序的设备的客户端驱动程序位于 IEEE 1394 驱动程序堆栈之上。 总线驱动程序提供了 IEEE 1394 总线的独立于硬件的界面。 设备驱动程序通过发送 Irp，处理的 IEEE 1394 总线驱动程序与设备进行通信。 在 Windows 7 之前总线驱动程序是端口驱动程序 (1394bus.sys) 和主板的主控制器 (ochi1394.sys) 的主微型端口驱动程序的组合。 在 Windows 7 和更高版本中，将由 1394ohci.sys，通过使用内核模式驱动程序框架 (KMDF) 实现的整体化 IEEE 1394 总线驱动程序替换旧端口/微型端口总线驱动程序。 1394ohci.sys 总线驱动程序是完全向后兼容旧的 1394年总线驱动程序。 有关一些新总线驱动程序和旧的 1394年总线驱动程序之间已知的行为差异的详细信息，请参阅[IEEE 1394 总线驱动程序在 Windows 7 中](https://msdn.microsoft.com/library/windows/hardware/gg266402)。

下图显示了旧和新的 1394年总线驱动程序之间的关系。

![显示旧和新的 1394年总线驱动程序之间的关系的关系图。](images/1394busdriver.png)

若要向连接到该总线的设备发出命令，驱动程序发出[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744) IRP，控制代码[ **IOCTL\_1394年\_类**](https://msdn.microsoft.com/library/windows/hardware/ff537232)。 驱动程序包中的 IEEE 1394 I/O 请求块的参数 ([**IRB**](https://msdn.microsoft.com/library/windows/hardware/ff537350))，并将指针传递给它在**Parameters.Others.Argument1** IRP 的成员。 **FunctionNumber** IRB 成员确定的操作，类型和**u**成员描述的操作。 总线驱动程序将使用 IOCTL\_1394年\_类 IRP 提供总线和主控制器的接口。

IRB 结构包含将应用于每个总线请求的参数和特定于请求的参数。 **U** IRB 成员包含中的数据结构，每个请求类型的其中一个并集的特定于请求的参数。

正常操作期间，驱动程序将接收普通的 I/O 请求 (如[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794))、 将它们转换为适当的 IEEE 1394 操作和调度，操作通过向设备 IOCTL\_1394年\_类。

## <a name="related-topics"></a>相关主题
[在 Windows 7 中的 IEEE 1394 总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/gg266402)  



