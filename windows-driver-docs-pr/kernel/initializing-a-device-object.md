---
title: 初始化设备对象
description: 初始化设备对象
ms.assetid: 97820c62-aade-4ae7-92a6-7490d0ad5697
keywords:
- 设备对象 WDK 内核，初始化
- 初始化设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613a76033869153ac4f1dc53df58eae8cb2b2847
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565805"
---
# <a name="initializing-a-device-object"></a>初始化设备对象





之后[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)返回时，为调用方提供一个指向*DeviceObject* ，其中包含一个指向[*设备扩展*](device-extensions.md)，驱动程序必须设置其各自的物理/逻辑，或虚拟设备的设备对象中的某些字段。

**IoCreateDevice**设置**StackSize**到一个新创建的设备对象的字段。 最低级别驱动程序可以忽略此字段。 在更高级别的驱动程序调用[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)若要将自身附加到下一步低驱动程序，该例程将自动设置**StackSize**字段中到其中的较低的下一步驱动程序的设备对象加 1 的设备对象。 对于某些设备类型，但是，更高级别的驱动程序可能需要设置**StackSize**到更大的价值，字段中的特定于设备的文档所述。 设置堆栈大小，可确保 Irp 发送到更高级别的驱动程序将包含一个特定于驱动程序的 I/O 堆栈位置，以及正确数量的链中的所有低级驱动程序的 I/O 堆栈位置。

**IoCreateDevice**设置**AlignmentRequirement**处理器的数据缓存行大小减 1，以确保在直接 I/O 中使用的缓冲区是否正确对齐到新创建的设备对象的字段。 之后**IoCreateDevice**返回时，最低级别的物理设备驱动程序必须执行以下操作：

1.  减一的对齐要求的设备。

2.  比较该结果与步骤 1 的当前值的设备对象的**AlignmentRequirement**。

3.  如果更高版本设备的对齐要求，则设置**AlignmentRequirement**到步骤 1 的结果。 否则，保持**AlignmentRequirement**所设置的值**IoCreateDevice**。

任何更高级别的驱动程序链接本身通过另一个驱动程序通过调用后[ **IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)，更高级别的驱动程序必须设置**AlignmentRequirement**的下一步低级驱动程序的设备对象的新创建的设备对象的字段。 作为一般规则，更高级别的驱动程序不应更改此值。 如果更高级别的驱动程序调用[ **IoAttachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548294)或[ **IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)，这些例程会自动设置**AlignmentRequirement**字段中的较低级驱动程序的设备对象的设备对象。

[**IoGetDeviceObjectPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff549198)较低级驱动程序的设备对象以及关联的文件对象返回的指针。 仅 FSD (也可能是另一个最高级别的驱动程序) 可以使用返回的文件对象指针。 调用的中间驱动程序**IoGetDeviceObjectPointer**应该保存此文件对象指针，以便它可以通过调用取消引用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)时该驱动程序被卸载。

FSD 装载包含表示较低的驱动程序的设备对象的文件对象的卷后，中间驱动程序无法链接本身之间的文件系统和较低的驱动程序通过调用**IoAttachDevice**或**IoAttachDeviceToDeviceStack**。 此外，可以设置 FSD **SectorSize**装入发生时的设备对象的成员基于基础卷硬件的几何图形上。 有关详细信息，请参阅[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)。

中间或最低级别的驱动程序还设置了一个位的设备对象中**标志**通过实现或运算它使用 DO\_直接\_IO 或使用\_缓冲\_IO 在每种设备对象创建。 逻辑或虚拟设备的最高级别的驱动程序可以避免设置**标志**为缓冲或直接 I/O 如果驱动程序编写器决定所涉及的其他工作即可更好的驱动程序性能。 中间的驱动程序必须设置**标志**字段以匹配的下一步低驱动程序的设备对象及其设备对象。

设置设备对象**标志**字段是否\_直接\_IO 或 DO\_缓冲\_IO 确定如何在 I/O 管理器访问到所有数据传输中的用户缓冲区将请求传递随后发送到该驱动程序。

驱动程序然后可以在设备对象中设置设备相关的任何其他值。 例如，可移动媒体设备的非 WDM 驱动程序必须 OR 设备对象的**标志**使用的成员\_验证\_卷如果检测到 （或怀疑） 在 I/O 操作期间的媒体中的更改。 (请参阅[支持可移动介质](supporting-removable-media.md)有关详细信息。)需要浪涌电源的设备的驱动程序必须或**标志**使用的成员\_POWER\_浪涌，且不在系统分页路径的设备的驱动程序必须或**标志**使用成员\_电源\_PAGABLE。 函数和筛选器驱动程序必须清除 DO\_设备\_正在初始化标志。

初始化后的设备对象，驱动程序还初始化任何内核定义的对象和它为其提供存储设备扩展在其他系统定义的数据结构。 准确地说时驱动程序执行以下任务取决于其设备，该对象的类型和/或数据的性质。 一般情况下，在中初始化任何对象或数据结构，并可以保留通过即插即用的开始和停止请求[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。 要求使用即插即用提供的资源信息的那些[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求，或该设备时，可能需要更改停止和/或重新启动，当驱动程序处理时应初始化**IRP\_MN\_启动\_设备**请求。 有关详细信息*AddDevice*例程，请参阅[编写 AddDevice 例程](writing-an-adddevice-routine.md)。

 

 




