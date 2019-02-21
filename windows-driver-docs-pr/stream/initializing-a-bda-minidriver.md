---
title: 初始化 BDA 微型驱动程序
description: 初始化 BDA 微型驱动程序
ms.assetid: 4df2efc6-e666-48d5-9a7b-cbf724c027f0
keywords:
- BDA 微型驱动程序 WDK AVStream 初始化
- 初始化 BDA 微型驱动程序 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e754275b219ff69618bff98b713bec62b681d213
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546235"
---
# <a name="initializing-a-bda-minidriver"></a>初始化 BDA 微型驱动程序





同样 BDA 微型驱动程序初始化为其他 AVStream 微型驱动程序。 BDA 微型驱动程序的驱动程序入口函数调用 AVStream [ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683)函数以初始化 BDA 微型驱动程序的驱动程序对象。 在此调用，BDA 微型驱动程序将传递一个指向[ **KSDEVICE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff561691)结构，它指定特征的设备，这可能包括：

-   一个指向[ **KSDEVICE\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff561693)包含 BDA 设备的调度表的结构。 BDA 微型驱动程序应至少提供创建和启动设备，并指定这些例程中的例程**外**并**启动**成员分别 KSDEVICE\_调度结构。 BDA 微型驱动程序的创建例程应设备类分配内存并引用指向指针[ **KSDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff561681) BDA 设备连接到此设备类的结构。 BDA 微型驱动程序的启动例程应从注册表获取有关设备的信息、 设置设备的相关信息和 BDA 支持库注册的静态模板结构的组。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)有关详细信息。

-   一个数组[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)支持此设备的单个筛选器类型的结构。 此结构类型描述由给定筛选器工厂创建的筛选器的特征。 如果您创建您 BDA 微型驱动程序，以便它不使用 BDA 支持库，应在此数组中指定的此类型的结构的成员 (*Bdasup.lib*) 来处理你 BDA 微型驱动程序的属性和方法集。 如果您创建您 BDA 微型驱动程序，以便它使用 BDA 支持库，然后在 BDA 微型驱动程序应改为调用[ **BdaCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff556438)支持函数以添加筛选器工厂描述符 （KSFILTER\_描述符结构) 为你的设备。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)有关详细信息。

下面的代码段显示了筛选器描述符的数组、 调度表以获取 BDA 设备和 BDA 设备描述符的示例：

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

 

 




