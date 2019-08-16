---
title: I/O 请求数据包
description: I/O 请求数据包
ms.assetid: 72288D9A-86F7-4145-8470-FFA1AC26E9BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d61c83d5f2403d57b7e266172f37db0762a797f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371955"
---
# <a name="io-request-packets"></a>I/O 请求数据包


发送到设备驱动程序的大部分请求都打包在 I/O 请求数据包 ([**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)) 中。 操作系统组件或驱动程序将 IRP 发送到驱动程序，方法是调用 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)，它有两个参数：指向 [**DEVICE\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object) 的指针和指向 **IRP** 的指针。 **DEVICE\_OBJECT** 具有指向关联 [**DRIVER\_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object) 的指针。 当组件调用 **IoCallDriver** 时，我们说组件“将 IRP 发送到设备对象”  或“将 IRP 发送到与设备对象关联的驱动程序”  。 有时，我们使用短语“传递 IRP”  或“转发 IRP”  而非“发送 IRP”  。

通常，IRP 由在堆栈中排列的多个驱动程序进行处理。 堆栈中的每个驱动程序都与一个设备对象相关联。 有关详细信息，请参阅[设备节点和设备堆栈](device-nodes-and-device-stacks.md)。 如果 [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp) 由设备堆栈进行处理，则通常先将 **IRP** 发送至设备堆栈中的顶部设备对象。 例如，如果 **IRP** 由此图所示的设备堆栈进行处理，则会先将 IRP 发送至设备堆栈顶部的筛选器设备对象（筛选器 DO）。

![设备节点及其设备堆栈的示意图](images/prosewaredevicenode03.png)

## <a name="span-idpassing_an_irp_down_the_device_stackspanspan-idpassing_an_irp_down_the_device_stackspanspan-idpassing_an_irp_down_the_device_stackspanpassing-an-irp-down-the-device-stack"></a><span id="Passing_an_IRP_down_the_device_stack"></span><span id="passing_an_irp_down_the_device_stack"></span><span id="PASSING_AN_IRP_DOWN_THE_DEVICE_STACK"></span>沿着设备堆栈向下传递 IRP


假设 I/O 管理器将 IRP 发送至图中的筛选器 DO。 与筛选器 DO 关联的驱动程序 AfterThought.sys 处理 IRP，然后将其传递至功能设备对象 (FDO)，该对象是设备堆栈中下一个低层设备对象。 当驱动程序将 IRP 传递至设备堆栈中下一个低层设备对象时，我们说驱动程序“沿着设备堆栈向下传递 IRP”  。

某些 IRP 会沿着设备堆栈一路向下传递至物理设备对象 (PDO)。 其他 IRP 从未到达 PDO，因为这些 IRP 由 PDO 上面的驱动程序之一完成。

## <a name="span-idirps_are_self-containedspanspan-idirps_are_self-containedspanspan-idirps_are_self-containedspanirps-are-self-contained"></a><span id="IRPs_are_self-contained"></span><span id="irps_are_self-contained"></span><span id="IRPS_ARE_SELF-CONTAINED"></span>IRP 为自包含


从某种意义上说，IRP 结构是自包含结构，因为它包含驱动程序处理 I/O 请求所需的所有信息。 IRP 结构的某些部分包含堆栈中所有参与驱动程序共同的信息。 IRP 的其他部分包含特定于堆栈中特定驱动程序的信息。

 

 





