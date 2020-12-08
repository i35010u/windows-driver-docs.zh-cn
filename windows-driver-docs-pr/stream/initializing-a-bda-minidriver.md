---
title: 初始化 BDA 微型驱动程序
description: 初始化 BDA 微型驱动程序
keywords:
- BDA 微型驱动程序 WDK AVStream，初始化
- 初始化 BDA 微型驱动程序 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c088c81af87bca0fd7ebe1ba3e2c9b4593ef95b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818771"
---
# <a name="initializing-a-bda-minidriver"></a>初始化 BDA 微型驱动程序





BDA 微型驱动程序的初始化方式类似于其他 AVStream 微型驱动程序。 BDA 微型驱动程序的 DriverEntry 函数调用 AVStream [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) 函数以初始化 BDA 微型驱动程序的驱动程序对象。 在此调用中，BDA 微型驱动程序传递指向指定设备特征的 [**KSDEVICE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor) 结构的指针，其中可能包括：

-   指向 [**KSDEVICE \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch) 结构的指针，该结构包含 BDA 设备的调度表。 BDA 微型驱动程序应该至少提供用于创建和启动设备的例程，并分别在 " **添加** " 和 " **启动** " 成员中指定 KSDEVICE \_ 调度结构。 BDA 微型驱动程序的 create 例程应为设备类分配内存，并将指向该 BDA 设备的 [**KSDEVICE**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice) 结构的指针引用到此设备类。 BDA 微型驱动程序的启动例程应从注册表获取有关设备的信息、设置有关设备的信息，然后使用 BDA 支持库注册一组静态模板结构。 有关详细信息，请参阅 [启动 BDA 微型驱动程序](starting-a-bda-minidriver.md) 。

-   此设备支持的各个筛选器类型的 [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor) 结构的数组。 此结构类型描述了给定筛选器工厂创建的筛选器的特征。 如果创建的是 BDA 微型驱动程序，使其不使用 BDA 支持库 (*Bdasup*) 来处理 bda 微型驱动程序的属性和方法集，则应在此数组中指定此类型的结构的成员。 如果创建的是 BDA 微型驱动程序，使其能够使用 BDA 支持库，则 BDA 微型驱动程序应改为调用 [**BdaCreateFilterFactory**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory) 支持函数来添加筛选器工厂描述符 (\_ 设备的 KSFILTER 描述符结构) 。 有关详细信息，请参阅 [启动 BDA 微型驱动程序](starting-a-bda-minidriver.md) 。

下面的代码片段演示了一个筛选器描述符数组的示例、一个 BDA 设备的一个调度表以及 BDA 设备的描述符：

```cpp
//
//  Array containing descriptors for all filter factories
//  available on the device.
//
//  Note!  Only used when dynamic topology is not used (that is, 
//         only when filters and pins are fixed). Typically, this 
//         is when the network provider is not present.
//
DEFINE_KSFILTER_DESCRIPTOR_TABLE(FilterDescriptors)
{
    &TemplateTunerFilterDescriptor
};
//
//  Device Dispatch Table
//
//  Lists the dispatch routines for the major events related to 
//  the underlying device.
//
extern
const
KSDEVICE_DISPATCH
DeviceDispatch =
{
    CDevice::Create,    // Add
    CDevice::Start,     // Start
    NULL,               // PostStart
    NULL,               // QueryStop
    NULL,               // CancelStop
    NULL,               // Stop
    NULL,               // QueryRemove
    NULL,               // CancelRemove
    NULL,               // Remove
    NULL,               // QueryCapabilities
    NULL,               // SurpriseRemoval
    NULL,               // QueryPower
    NULL                // SetPower
};
//
//  Device Descriptor
//
//  Brings together the data structures that define the device and
//  the initial filter factories that can be created on it.
//  Note that because template topology structures are specific 
//  to BDA, the device descriptor does not include them.
//  Note also that if BDA dynamic topology is used, the device 
//  descriptor does not specify a list of filter factory descriptors.
//  If BDA dynamic topology is used, the BDA minidriver calls 
//  BdaCreateFilterFactory to add filter factory descriptors. 
extern
const
KSDEVICE_DESCRIPTOR
DeviceDescriptor =
{
    &DeviceDispatch,    // Dispatch
#ifdef DYNAMIC_TOPOLOGY // network provider is present
    0,    // FilterDescriptorsCount
    NULL, // FilterDescriptors
#else     // network provider is not present
    SIZEOF_ARRAY( FilterDescriptors), // FilterDescriptorsCount
    FilterDescriptors                 // FilterDescriptors
#endif // DYNAMIC_TOPOLOGY
```

 

