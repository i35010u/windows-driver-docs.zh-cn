---
title: 初始化设备对象
description: 初始化设备对象
keywords:
- 设备对象 WDK 内核，初始化
- 初始化设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8b5bef194de38178256ca0e7b4c1536188734e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837709"
---
# <a name="initializing-a-device-object"></a>初始化设备对象





[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)返回后，为调用方提供一个指向 *DeviceObject* 的指针，该指针包含指向 [*设备扩展*](device-extensions.md)的指针，驱动程序必须在设备对象中为其各自的物理、逻辑和/或虚拟设备设置某些字段。

**IoCreateDevice** 将新创建的设备对象的 **StackSize** 字段设置为1。 最低级别的驱动程序可以忽略此字段。 当更高级别的驱动程序调用 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 将自身附加到下一个较低的驱动程序时，该例程会自动将设备对象中的 **StackSize** 字段设置为下一个较低驱动程序的设备对象加1。 但对于某些设备类型，更高级别的驱动程序可能需要将 " **StackSize** " 字段设置为更大的值，如设备特定文档中所述。 设置堆栈大小可确保发送到更高级别的驱动程序的 Irp 将包含特定于驱动程序的 i/o 堆栈位置，以及链中所有较低级别驱动程序的 i/o 堆栈位置的正确数目。

**IoCreateDevice** 将新创建的设备对象的 **AlignmentRequirement** 字段设置为处理器的数据缓存行大小减一，以确保直接 i/o 中使用的缓冲区对齐正确。 **IoCreateDevice** 返回后，最低级别的物理设备驱动程序必须执行以下操作：

1.  从设备的对齐要求中减去一个。

2.  将步骤1的结果与设备对象的 **AlignmentRequirement** 的当前值进行比较。

3.  如果设备的对齐要求更大，请将 **AlignmentRequirement** 设置为步骤1的结果。 否则，保留 **IoCreateDevice** 设置的 **AlignmentRequirement** 值。

通过调用 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)，在任何更高级别的驱动程序通过其他驱动程序将其链接到其他驱动程序之后，更高级别的驱动程序必须将其新创建的设备对象的 AlignmentRequirement 字段设置为下一个较低级别驱动程序的设备对象的 " **AlignmentRequirement** " 字段。 作为一般规则，较高级别的驱动程序不应更改此值。 如果较高级别的驱动程序调用 [**IoAttachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)或 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)，则这些例程会自动将设备对象中的 AlignmentRequirement 字段设置为较低级别驱动程序的设备对象的 **AlignmentRequirement** 字段。

[**Plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 将指针同时返回到低级驱动程序的设备对象和关联的文件对象。 只有 FSD (或另一个最高级别的驱动程序) 才能使用返回的文件对象指针。 调用 **plxntb** 的中间驱动程序应保存此文件对象指针，以便在卸载驱动程序时通过调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 来取消对该指针的引用。

FSD 装载了包含表示较低驱动程序的设备对象的文件对象的卷之后，中间驱动程序无法通过调用 **IoAttachDevice** 或 **IoAttachDeviceToDeviceStack** 在文件系统和低级驱动程序之间链接自身。 此外，FSD 可以根据安装发生时的基础卷硬件的几何设置设备对象的 **SectorSize** 成员。 有关详细信息，请参阅 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)。

中级或低级驱动程序还会通过 **Flags** \_ \_ \_ \_ 在其创建的每个设备对象中使用 "执行直接 IO" 或 "执行缓冲 IO" or 来设置设备对象标志中的位。 如果驱动程序编写器决定涉及的附加工作，则逻辑或虚拟设备的最高级别驱动程序可以避免为缓冲或直接 i/o 设置 **标志** 。 中间驱动程序必须将其设备对象的 "标志" 字段设置为与下一个较低驱动程序的设备对象的 " **标志** " 字段相匹配。

使用 "执行 **Flags** \_ 直接 IO" 或 "缓冲 IO" 设置设备对象标志字段 \_ \_ \_ 决定了在随后发送到驱动程序的所有数据传输请求中，i/o 管理器如何传递对用户缓冲区的访问权限。

然后，驱动程序可以在设备对象中设置任何其他设备相关值。 例如，如果使用可移动媒体设备的非 WDM 驱动程序，或设备对象的 **Flags** 成员 \_ \_ 检测 (到在 i/o 操作期间) 介质的更改，则必须具有 "确实验证" 卷。 有关详细信息，请参阅 [支持可移动媒体](supporting-removable-media.md) (。 ) 需要浪涌电源的设备的驱动程序必须或带有 do 电涌的 **标志** 成员 \_ \_ ，并且不在系统分页路径中的设备驱动程序必须或带有 do power PAGABLE 的 **flags** 成员 \_ \_ 。 函数和筛选器驱动程序必须清除 "执行 \_ 设备 \_ 初始化" 标志。

初始化设备对象之后，驱动程序还可以初始化任何内核定义的对象和其他系统定义的数据结构，在设备扩展中它为其提供存储。 驱动程序执行这些任务的确切时间取决于其设备、对象的类型和/或数据的性质。 通常，可通过 PnP 开始和停止请求持久保存的任何对象或数据结构都可以在 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中进行初始化。 当驱动程序处理 **IRP \_ MN \_ START \_ device** 请求时，需要使用 PnP [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)请求提供的资源信息，或者可能需要更改的那些资源信息。 有关 *AddDevice* 例程的详细信息，请参阅 [编写 AddDevice 例程](writing-an-adddevice-routine.md)。

 

