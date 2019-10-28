---
title: MSiSCSI\_RequestTimeStatistics WMI 类
description: MSiSCSI\_RequestTimeStatistics WMI 类
ms.assetid: 3e9f3214-3120-41f6-bb06-7ace4f243c5f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e38a81799f0ada4c7478ff4cc96522b3714178c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838874"
---
# <a name="msiscsi_requesttimestatistics-wmi-class"></a>MSiSCSI\_RequestTimeStatistics WMI 类


MSiSCSI\_RequestTimeStatistics WMI 类提供有关 iSCSI 请求的统计信息。 此类在*管理 mof*中定义为：

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

当 WMI 工具套件编译上述类定义时，它会生成[**MSiSCSI\_RequestTimeStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_requesttimestatistics)数据结构。

 

 





