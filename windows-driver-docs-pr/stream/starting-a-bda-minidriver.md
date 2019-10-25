---
title: 启动 BDA 微型驱动程序
description: 启动 BDA 微型驱动程序
ms.assetid: c71e1483-756c-4e98-a413-64ff02ee4a9b
keywords:
- BDA 微型驱动程序 WDK AVStream，正在启动
- 启动 BDA 微型驱动程序 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb26d511dd464ceb3213af7d50252872355c6104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837700"
---
# <a name="starting-a-bda-minidriver"></a>启动 BDA 微型驱动程序





当 BDA 设备开始运行时，即插即用（PnP）管理器将[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)。 AVStream 类又调用与 BDA 设备关联的 BDA 微型驱动程序的启动例程。 此开始例程将从注册表中检索有关设备的信息、设置有关设备的信息，然后调用[**BdaCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory)支持函数来执行以下操作：

-   从设备的初始筛选器描述符（[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)）为设备创建筛选器工厂。 初始筛选器描述符引用 "筛选器" 和 "输入插针" 的调度和自动化表。 有关详细信息，请参阅[创建调度表](creating-dispatch-tables.md)和[定义自动化表](defining-automation-tables.md)。

-   将筛选器工厂与[**BDA\_筛选器相关联\_模板**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)结构。 此结构引用设备的模板筛选器描述符以及可能的输入插针和输出插针对的列表。 此描述符和列表依次引用：
    -   网络提供程序可用于确定 BDA 筛选器拓扑的静态模板结构。
    -   用于 BDA 筛选器的节点和 pin 以及连接筛选器的可能方法。
    -   网络提供程序可用于创建和关闭筛选器实例的例程。
    -   网络提供程序可用于处理 BDA 筛选器的静态模板结构。
-   使用 BDA 支持库注册由 BDA\_筛选器指定的静态模板结构\_模板，使库可以为 BDA 微型驱动程序的属性和方法提供默认处理。

以下代码片段显示了**BdaCreateFilterFactory**设置为筛选器工厂的设备的初始筛选器描述符的示例：

```cpp
const KSFILTER_DESCRIPTOR    InitialTunerFilterDescriptor;
//
//  Filter Factory Descriptor for the tuner filter
//
//  This structure brings together all of the structures that define
//  the tuner filter instance as it appears when it is first created.
//  Note that not all template pin and node types are exposed as
//  pin and node factories when the filter instance is created.
//
DEFINE_KSFILTER_DESCRIPTOR(InitialTunerFilterDescriptor)
{
    &FilterDispatch,             // Table of dispatch routines
    &FilterAutomation,           // Table of properties and methods
    KSFILTER_DESCRIPTOR_VERSION, // Version
    0,                           // Flags
    &KSNAME_Filter,              // Reference Guid
    DEFINE_KSFILTER_PIN_DESCRIPTORS(InitialPinDescriptors),
                                   // PinDescriptorsCount
                                   // PinDescriptorSize
                                   // PinDescriptors
    DEFINE_KSFILTER_CATEGORY(KSCATEGORY_BDA_RECEIVER_COMPONENT),
                            // CategoriesCount
                            // Categories
    DEFINE_KSFILTER_NODE_DESCRIPTORS_NULL(NodeDescriptors),
                                    // NodeDescriptorsCount
                                    // NodeDescriptorSize
                                    // NodeDescriptors
    DEFINE_KSFILTER_DEFAULT_CONNECTIONS, // ConnectionsCount
                                         // Connections
    NULL                // ComponentId
};
```

下面的代码片段演示一个由初始化的筛选器公开的初始 pin 说明符数组的示例。 网络提供程序在网络提供程序配置该筛选器之前使用此类数组初始化筛选器。 但是，在配置已初始化的筛选器时，网络提供程序会选择指向 BDA\_筛选器的筛选器描述符成员的指针中引用的 pin\_模板结构。 有关详细信息，请参阅[配置 BDA 筛选器](configuring-a-bda-filter.md)。

```cpp
//
//  Initial Pin Descriptors
//
//  This data structure defines the pins that will appear on the 
//  filter when it is first created.
//
const
KSPIN_DESCRIPTOR_EX
InitialPinDescriptors[] =
{
    //  Antenna Pin
    //
    {
        &AntennaPinDispatch,
        &AntennaAutomation,   // AntennaPinAutomation
        {
            0,  // Interfaces
            NULL,
            0,  // Mediums
            NULL,
            SIZEOF_ARRAY(AntennaPinRanges),
            AntennaPinRanges,
            KSPIN_DATAFLOW_IN,
            KSPIN_COMMUNICATION_BOTH,
            NULL,   // Name
            NULL,   // Category
            0
        },
        KSPIN_FLAG_DO_NOT_USE_STANDARD_TRANSPORT | 
        KSPIN_FLAG_FRAMES_NOT_REQUIRED_FOR_PROCESSING | 
        KSPIN_FLAG_FIXED_FORMAT,
        1,      // InstancesPossible
        0,      // InstancesNecessary
        NULL,   // Allocator Framing
        NULL    // PinIntersectHandler
    }
};
```

请注意，已初始化的筛选器必须公开一个或多个输入插针，以便 Microsoft DirectShow **IFilterMapper2**或**IFilterMapper**接口可以找到该筛选器。 请参阅 Microsoft Windows SDK 文档，获取有关这些 DirectShow 接口的信息。

下面的代码片段演示了一个 "BDA\_筛选器"\_模板结构和相关结构和数组的示例：

```cpp
const KSFILTER_DESCRIPTOR  TemplateTunerFilterDescriptor;
const BDA_PIN_PAIRING  *TemplateTunerPinPairings;
//
//  BDA Template Topology Descriptor for the filter factory.
//
//  This structure defines the pin and node types that the network 
//  provider can create on the filter and how they are arranged. 
//
const
BDA_FILTER_TEMPLATE
TunerBdaFilterTemplate =
{
    &TemplateTunerFilterDescriptor,
    SIZEOF_ARRAY(TemplateTunerPinPairings),
    TemplateTunerPinPairings
};
//
//  Filter Factory Descriptor for the tuner filter template topology
//
//  This structure brings together all of the structures that define
//  the topologies that the tuner filter can assume as a result of
//  pin factory and topology creation methods.
//
DEFINE_KSFILTER_DESCRIPTOR(TemplateTunerFilterDescriptor)
{
    &FilterDispatch,             // Table of dispatch routines
    &FilterAutomation,           // Table of properties and methods
    KSFILTER_DESCRIPTOR_VERSION, // Version
    0,                           // Flags
    &KSNAME_Filter,              // Reference Guid
    DEFINE_KSFILTER_PIN_DESCRIPTORS(TemplatePinDescriptors),
                                   // PinDescriptorsCount
                                   // PinDescriptorSize
                                   // PinDescriptors
    DEFINE_KSFILTER_CATEGORY(KSCATEGORY_BDA_RECEIVER_COMPONENT),
                            // CategoriesCount
                            // Categories
    DEFINE_KSFILTER_NODE_DESCRIPTORS(NodeDescriptors),  
                                    // NodeDescriptorsCount
                                    // NodeDescriptorSize
                                    // NodeDescriptors
    DEFINE_KSFILTER_CONNECTIONS(TemplateTunerConnections),
                               // ConnectionsCount
                               // Connections
    NULL                // ComponentId
};
//
//  Lists how pairs of input and output pins are configured. 
//
//  Values given to the BDA_PIN_PAIRING structures in the list inform 
//  the network provider which nodes get duplicated when more than one 
//  output pin type is connected to a single input pin type or when
//  more that one input pin type is connected to a single output pin 
//  type. Also, informs of the joints array.
//
const
BDA_PIN_PAIRING TemplateTunerPinPairings[] =
{
    //  Antenna to Transport Topology Joints
    //
    {
        0,  // ulInputPin
        1,  // ulOutputPin
        1,  // ulcMaxInputsPerOutput
        1,  // ulcMinInputsPerOutput
        1,  // ulcMaxOutputsPerInput
        1,  // ulcMinOutputsPerInput
        SIZEOF_ARRAY(AntennaTransportJoints),   // ulcTopologyJoints
        AntennaTransportJoints                  // pTopologyJoints
    }
};
```

 

 




