---
title: 定义自动化表
description: 定义自动化表
ms.assetid: 1c0dace6-b618-4705-bf5d-65457d14c072
keywords:
- BDA 微型驱动程序 WDK AVStream，自动化表
- 自动化表 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9944d2f233d8c8e478a629399ed8d4e2d5cbf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540951"
---
# <a name="defining-automation-tables"></a>定义自动化表





用于筛选器、 pin 或节点的自动化表是什么描述的属性和方法支持的筛选器、 pin 或节点。 如果 BDA 微型驱动程序提供的属性或方法的处理程序已由 AVStream，BDA 微型驱动程序的实现取代 AVStream 的。

BDA 微型驱动程序应定义的属性和方法集的数组，然后定义自动化表，这些设置数组以便微型驱动程序可以自动处理请求。 请参阅[确定 BDA 设备拓扑](determining-bda-device-topology.md)部分，了解如何微型驱动程序还定义的属性设置为本部分中所引用的示例。

下面的代码段显示了筛选器自动化表的示例，以及属性和方法集的数组：

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

下面的代码段显示了节点自动化表的示例和数组的属性集的：

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

 

 




