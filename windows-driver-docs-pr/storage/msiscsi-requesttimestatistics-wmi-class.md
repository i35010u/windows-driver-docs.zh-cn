---
title: MSiSCSI \_ REQUESTTIMESTATISTICS WMI 类
description: MSiSCSI \_ REQUESTTIMESTATISTICS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2db6450e116719e8a7b90aa8cd75bb6ea1f6cf3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796451"
---
# <a name="msiscsi_requesttimestatistics-wmi-class"></a>MSiSCSI \_ REQUESTTIMESTATISTICS WMI 类


MSiSCSI \_ REQUESTTIMESTATISTICS WMI 类提供有关 iSCSI 请求的统计信息。 此类在 *管理 mof* 中定义为：

```cpp
class MSiSCSI_RequestTimeStatistics : Win32_PerfRawData
{
    [read,key] String InstanceName;
    [read] boolean Active;


    [read,
     WmiDataId(1),
     WmiVersion(1),
     description("Name of the iSCSI Target"),
     MaxLen(MAX_ISCSI_NAME_LEN)] string iSCSIName;

    [read,
     WmiDataId(2),
     WmiVersion(1),
     Description("The iSCSI connection ID for this connection instance."): amended
    ] uint16 CID; //session wide namespace

    [read,
     WmiDataId(3),
     Description("A uniquely generated session ID used only internally.  This is the value returned by the LoginToTarget method."): amended,
     WmiVersion(1)] uint64 USID;

    [WmiDataId(4),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     description("Id that is globally unique to each instance of each adapter. This is the value reported by the MSiSCSI_HBAInformation class.") : amended
    ]
    uint64 UniqueAdapterId;

    [WmiDataId(5),
    DisplayName("Max Request Processing Time"): amended,
    PerfDefault,
    CounterType(PERF_COUNTER_BULK_COUNT),
    DefaultScale(0),
    PerfDetail(100),
    read,
    Description("Maximum time taken to process a request over this connection"): amended
    ] uint32 MaximumProcessingTime;

    [WmiDataId(6),
    DisplayName("Average Request Processing Time"): amended,
    PerfDefault,
    CounterType(PERF_COUNTER_BULK_COUNT),
    DefaultScale(0),
    PerfDetail(100),
    read,
    Description("Average time taken to process a request over this connection"): amended
    ] uint32 AverageProcessingTime;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ RequestTimeStatistics**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_requesttimestatistics) 数据结构。

 

