---
title: 映射连接拓扑
description: 映射连接拓扑
ms.assetid: f11ffc48-a117-4b75-bc19-7a3762e6ba19
keywords:
- 方法设置 WDK BDA，映射连接拓扑
- 属性设置 WDK BDA，映射连接拓扑
- 拓扑 WDK BDA
- 映射连接拓扑
- 连接拓扑映射 WDK BDA
- BDA_TEMPLATE_CONNECTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc9389e13c27645bfee7e1cc81b88a6a0ec2f610
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185861"
---
# <a name="mapping-connection-topology"></a>映射连接拓扑





为了使 BDA 支持库代表 BDA 微型驱动程序向第3环中的应用程序提供属性和方法，BDA 微型驱动程序必须提供其连接拓扑到 BDA 支持库的映射。 BDA 微型驱动程序提供 [**bda \_ 模板 \_ 连接**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection) 结构数组中的此映射。 当 BDA 微型驱动程序 \_ \_ 调用[**BdaCreateFilterFactory**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory)支持函数时，它会在[**KSTOPOLOGY \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)结构数组中传递此 bda 模板连接数组。 有关详细信息，请参阅 [启动 BDA 微型驱动程序](starting-a-bda-minidriver.md) 。 此数组提供了可在筛选器之间或筛选器与相邻筛选器之间进行的节点和 pin 类型之间的所有可能连接的表示形式。

然后，网络提供程序筛选器可以对 \_ \_ \_ BDA 微型驱动程序的筛选器实例上设置的 [KSPROPSETID \_ BdaTopology](./kspropsetid-bdatopology.md) 属性请求 KSPROPERTY 的 bda 模板连接属性请求，以检索微型驱动程序的连接拓扑。 BDA 微型驱动程序将调用 [**BdaPropertyTemplateConnections**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertytemplateconnections) 支持函数，该函数将返回筛选器的模板连接列表， (BDA \_ 模板 \_ 连接结构在 KSTOPOLOGY 连接结构数组中) \_ 。 BDA \_ 模板连接结构的成员 \_ 识别连接的以下对节点和固定类型：

-   连接开始处的节点和固定类型

-   连接结束的节点和固定类型

将节点类型设置为值−1表示连接在上游或下游筛选器的 pin 上分别开始或结束。 否则，节点类型的值对应于内部节点类型的从零开始的数组中的元素的索引。 此数组是 [**KSNODE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor) 结构的数组。 固定类型的值对应于从零开始的 pin 类型数组中的元素索引，这些类型可用于 BDA 微型驱动程序的模板筛选器描述符。 此数组是 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 结构的数组。

以下代码片段显示了可在 "BDA 微型驱动程序" 的模板筛选器描述符中使用的节点类型和固定类型的示例数组：

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

以下代码片段显示了模板连接和连接的数组的示例：

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

 

