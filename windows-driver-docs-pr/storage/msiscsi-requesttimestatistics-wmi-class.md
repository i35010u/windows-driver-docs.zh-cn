---
title: MSiSCSI\_RequestTimeStatistics WMI 类
description: MSiSCSI\_RequestTimeStatistics WMI 类
ms.assetid: 3e9f3214-3120-41f6-bb06-7ace4f243c5f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 22262d757e3d5a0f2d447ed11a75e1fd56849cd5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384671"
---
# <a name="msiscsirequesttimestatistics-wmi-class"></a>MSiSCSI\_RequestTimeStatistics WMI 类


MSiSCSI\_RequestTimeStatistics WMI 类提供了有关 iSCSI 的请求统计信息。 此类定义，如下所示在*Mgmt.mof。*

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_RequestTimeStatistics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiprf/ns-iscsiprf-_msiscsi_requesttimestatistics)数据结构。

 

 





