---
title: 映射连接拓扑
description: 映射连接拓扑
ms.assetid: f11ffc48-a117-4b75-bc19-7a3762e6ba19
keywords:
- 方法设置 WDK BDA，映射连接拓扑
- 属性设置 WDK BDA，映射连接拓扑
- 拓扑 WDK BDA
- 映射连接拓扑
- 映射 WDK BDA 连接拓扑
- BDA_TEMPLATE_CONNECTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd11de6cf3cbccd37b04b84ee44ab2ba2b87f472
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391381"
---
# <a name="mapping-connection-topology"></a>映射连接拓扑





为了使 BDA 支持库提供属性和方法添加到应用程序中的 3 环代表 BDA 微型驱动程序，BDA 微型驱动程序必须提供其到 BDA 支持库的连接拓扑的映射。 BDA 微型驱动程序提供了一个数组中的此映射[ **BDA\_模板\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff556558)结构。 BDA 微型驱动程序将传递此 BDA\_模板\_连接数组中的数组[ **KSTOPOLOGY\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff567148)结构时，它调用[ **BdaCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff556438)支持函数。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)有关详细信息。 此数组提供的表示形式可在筛选器或筛选器和相邻的筛选器之间的节点和 pin 类型之间的所有可能的连接。

网络提供程序筛选器可以随后进行 KSPROPERTY\_BDA\_模板\_的连接属性请求[KSPROPSETID\_BdaTopology](https://msdn.microsoft.com/library/windows/hardware/ff566561)对筛选器设置属性若要检索微型驱动程序的连接拓扑 BDA 微型驱动程序的实例。 BDA 微型驱动程序将调用[ **BdaPropertyTemplateConnections** ](https://msdn.microsoft.com/library/windows/hardware/ff556501)支持函数，返回列表的筛选器的模板连接 (BDA\_模板\_连接结构) 数组中的 KSTOPOLOGY\_连接结构。 成员 BDA\_模板\_连接结构标识以下对节点和 pin 的连接类型：

-   连接的开始处的节点和 pin 码类型

-   连接结束的位置的节点和 pin 码类型

节点类型设置为 − 1 的值指示连接开始或结束于上游或下游筛选 pin 分别。 否则，节点类型的值对应于内部节点类型的从零开始的数组中元素的索引。 此数组是一个数组[ **KSNODE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563473)结构。 Pin 类型的值对应于 pin BDA 微型驱动程序的模板筛选器描述符中可用的类型的从零开始的数组中元素的索引。 此数组是一个数组[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。

下面的代码段显示了示例中，节点类型和可用 BDA 微型驱动程序模板筛选器描述符中的固定类型的数组：

```cpp
//
//  Template Node Descriptors
//
//  This array describes all Node Types available in the template
//  topology of the filter.
//
const
KSNODE_DESCRIPTOR
NodeDescriptors[] =
{
    {   // 0 node type
        &RFTunerNodeAutomation,// PKSAUTOMATION_TABLE AutomationTable;
        &KSNODE_BDA_RF_TUNER,  // Type
        NULL                   // Name
    },
    {   // 1 node type
        &VSB8DemodulatorNodeAutomation, // PKSAUTOMATION_TABLE 
                                        // AutomationTable;
        &KSNODE_BDA_8VSB_DEMODULATOR,   // Type
        NULL                            // Name
    }
};
//
//  Template Pin Descriptors
//
//  This data structure defines the pin types available in the filters
//  template topology. These structures will be used to create a
//  pin factory ID for a pin type when BdaMethodCreatePin is called.
//
const
KSPIN_DESCRIPTOR_EX
TemplatePinDescriptors[] =
{
    //  Antenna Pin
    //  0 pin type
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
    },

    //  Transport Pin
    //  1 pin type
    {
        &TransportPinDispatch,
        &TransportAutomation,   // TransportPinAutomation
        {
            0,  // Interfaces
            NULL,
            1,  // Mediums
            &TransportPinMedium,
            SIZEOF_ARRAY(TransportPinRanges),
            TransportPinRanges,
            KSPIN_DATAFLOW_OUT,
            KSPIN_COMMUNICATION_BOTH,
            (GUID *) &PINNAME_BDA_TRANSPORT,   // Name
            (GUID *) &PINNAME_BDA_TRANSPORT,   // Category
            0
        },
        KSPIN_FLAG_DO_NOT_USE_STANDARD_TRANSPORT | 
        KSPIN_FLAG_FRAMES_NOT_REQUIRED_FOR_PROCESSING | 
        KSPIN_FLAG_FIXED_FORMAT,
        1,
        1,      // InstancesNecessary
        NULL,   // Allocator Framing
        NULL    // PinIntersectHandler
    }
};
```

下面的代码段显示了模板连接和关节的数组的示例：

```cpp
//
//  BDA Template Topology Connections
//
//  Lists the possible connections between pin types and
//  node types. This structure along with the BDA_FILTER_TEMPLATE, 
//  KSFILTER_DESCRIPTOR, and BDA_PIN_PAIRING structures 
//  describe how topologies are created in the filter.
//
const
KSTOPOLOGY_CONNECTION TemplateTunerConnections[] =
{
    { -1,  0,  0,  0}, // from upstream filter to 0 pin of 0 node 
    {  0,  1,  1,  0}, // from 1 pin of 0 node to 0 pin of 1 node 
    {  1,  1,  -1, 1}, // from 1 pin of 1 node to downstream filter 
};
//
//  Lists the template joints between antenna (input) and transport 
//  (output) pin types. Values given to joints correspond to indexes 
//  of elements in the preceding KSTOPOLOGY_CONNECTION array.
// 
//  For this template topology, the RF node (0) belongs to the antenna 
//  pin and the 8VSB demodulator node (1) belongs to the transport pin
//
const
ULONG   AntennaTransportJoints[] =
{
    1  // Second element in the preceding KSTOPOLOGY_CONNECTION array.
};
```

 

 




