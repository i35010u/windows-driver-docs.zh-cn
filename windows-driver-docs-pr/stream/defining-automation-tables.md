---
title: 定义自动化表
description: 定义自动化表
keywords:
- BDA 微型驱动程序 WDK AVStream，自动化表
- 自动化表 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d686430eb9373817c1a9dbe70dc26d1bceee98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817947"
---
# <a name="defining-automation-tables"></a>定义自动化表





筛选器、pin 或节点的自动化表描述了筛选器、pin 或节点支持的属性和方法。 如果 BDA 微型驱动程序提供已由 AVStream 实现的属性或方法处理程序，则 BDA 微型驱动程序的实现将取代 AVStream。

BDA 微型驱动程序应定义属性和方法集的数组，然后为这些集数组定义自动化表，以便微型驱动程序可以自动处理请求。 请参阅 [确定 BDA 设备拓扑](determining-bda-device-topology.md) 部分，了解微型驱动程序如何定义此部分所引用的属性集。

下面的代码片段演示了筛选器自动化表以及属性和方法集的数组的示例：

```cpp
//
//  Filter Level Property Set supported
//
//  This array defines a property set supported by the
//  filter that is exposed by the minidriver.
//
DEFINE_KSPROPERTY_SET_TABLE(FilterPropertySets)
{
    DEFINE_KSPROPERTY_SET
    (
        &KSPROPSETID_BdaTopology,                   // Set
        SIZEOF_ARRAY(FilterTopologyProperties),     // PropertiesCount
        FilterTopologyProperties,                   // PropertyItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Filter Level Method Sets supported
//
//  This array defines method sets supported by the
//  filter that is exposed by the minidriver.
//
DEFINE_KSMETHOD_SET_TABLE(FilterMethodSets)
{
    DEFINE_KSMETHOD_SET
    (
        &KSMETHODSETID_BdaChangeSync,               // Set
        SIZEOF_ARRAY(BdaChangeSyncMethods),         // MethodsCount
        BdaChangeSyncMethods,                       // MethodItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    ),
    DEFINE_KSMETHOD_SET
    (
        &KSMETHODSETID_BdaDeviceConfiguration,      // Set
        SIZEOF_ARRAY(BdaDeviceConfigurationMethods),// MethodsCount
        BdaDeviceConfigurationMethods,              // MethodItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Filter Automation Table
//
//  Lists all arrays of property and method sets for the filter that 
//  is exposed by the minidriver.
//
DEFINE_KSAUTOMATION_TABLE(FilterAutomation) {
    DEFINE_KSAUTOMATION_PROPERTIES(FilterPropertySets),
    DEFINE_KSAUTOMATION_METHODS(FilterMethodSets),
    DEFINE_KSAUTOMATION_EVENTS_NULL
};
```

下面的代码片段显示了一个节点自动化表和一组属性集的示例：

```cpp
//
//  RF tuner node property set supported
//
//  This array defines a property set supported by the
//  RF Tuner Node associated with the antenna input pin.
//
DEFINE_KSPROPERTY_SET_TABLE(RFNodePropertySets)
{
    DEFINE_KSPROPERTY_SET
    (
        &KSPROPSETID_BdaFrequencyFilter,            // Set
        SIZEOF_ARRAY(RFNodeFrequencyProperties),    // PropertiesCount
        RFNodeFrequencyProperties,                  // PropertyItems
        0,                                          // FastIoCount
        NULL                                        // FastIoTable
    )
};
//
//  Radio frequency tuner node automation table
//
//
DEFINE_KSAUTOMATION_TABLE(RFTunerNodeAutomation) {
    DEFINE_KSAUTOMATION_PROPERTIES( RFNodePropertySets),
    DEFINE_KSAUTOMATION_METHODS_NULL,
    DEFINE_KSAUTOMATION_EVENTS_NULL
};
```

 

 




