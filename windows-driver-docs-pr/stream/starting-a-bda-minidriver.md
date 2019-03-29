---
title: 启动 BDA 微型驱动程序
description: 启动 BDA 微型驱动程序
ms.assetid: c71e1483-756c-4e98-a413-64ff02ee4a9b
keywords:
- BDA 微型驱动程序 WDK AVStream，启动
- 启动 BDA 微型驱动程序 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a63e9266792f5248da35d7009b0f9970a8fd56e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577147"
---
# <a name="starting-a-bda-minidriver"></a>启动 BDA 微型驱动程序





BDA 设备启动时运行，插即用 (PnP) 管理器将调度[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)。 AVStream 类反过来调用 BDA 微型驱动程序与 BDA 设备相关联的启动例程。 此启动例程从注册表检索有关设备的信息，将有关设备的信息，然后调用[ **BdaCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff556438)支持到函数：

-   从初始的筛选器描述符创建设备筛选器工厂 ([**KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)) 设备。 初始的筛选器描述符引用筛选器和输入插针调度和自动化的表。 请参阅[创建调度表](creating-dispatch-tables.md)并[定义自动化表](defining-automation-tables.md)有关详细信息。

-   将与筛选器工厂相关联[ **BDA\_筛选器\_模板**](https://msdn.microsoft.com/library/windows/hardware/ff556523)结构。 此结构引用模板筛选器描述符，设备并对可能的输入和输出插针的列表。 此描述符和列表又引用：
    -   网络提供商可用于确定 BDA 筛选器的拓扑的静态模板结构。
    -   节点和 BDA 筛选器以及可能的方法连接筛选器的 pin。
    -   网络提供商可用于创建和关闭筛选器实例的例程。
    -   网络提供商可用于处理 BDA 筛选器的静态模板结构。
-   注册的静态模板结构所指定的 BDA\_筛选器\_BDA 模板支持库，以便库可以提供默认处理 BDA 微型驱动程序的属性和方法。

下面的代码段显示的设备是初始的筛选器描述符示例**BdaCreateFilterFactory**设置作为筛选器工厂：

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

下面的代码段显示了由初始化筛选器的初始 pin 描述符的数组的示例。 网络提供程序初始化之前的网络提供程序来配置该筛选器使用这样的数组的筛选器。 但是，在配置初始化筛选器时，网络提供商选择引用的 pin 中指向 BDA 的筛选器描述符成员的指针\_筛选器\_模板的结构。 请参阅[配置 BDA 筛选器](configuring-a-bda-filter.md)有关详细信息。

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

请注意，初始化筛选器必须有一个或多个输入插针公开，以便 Microsoft DirectShow **IFilterMapper2**或**IFilterMapper**接口可以找到该筛选器。 请参阅 Microsoft Windows SDK 文档，以了解有关这些 DirectShow 接口。

下面的代码段显示了示例的 BDA\_筛选器\_模板结构和相关的结构和数组：

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

 

 




