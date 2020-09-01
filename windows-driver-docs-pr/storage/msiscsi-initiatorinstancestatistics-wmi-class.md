---
title: MSiSCSI \_ INITIATORINSTANCESTATISTICS WMI 类
description: MSiSCSI \_ INITIATORINSTANCESTATISTICS WMI 类
ms.assetid: 5cb20302-e3f9-40fe-b501-7c23d284c120
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d13bff1ab6e90ecd4b7d36f5e9171fe78e115c1a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193179"
---
# <a name="msiscsi_initiatorinstancestatistics-wmi-class"></a>MSiSCSI \_ INITIATORINSTANCESTATISTICS WMI 类


## <span id="ddk_msiscsi_initiatorinstancestatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORINSTANCESTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI \_ INITIATORINSTANCESTATISTICS WMI 类公开发起方统计信息。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

MSiSCSI \_ InitiatorInstanceStatistics 类是在 *Iscsiprf*中定义的。

```cpp
class MSiSCSI_InitiatorInstanceStatistics : Win32_PerfRawData {
  [read,key] String InstanceName;
  [read] boolean Active;
  [WmiDataId(1),
    DisplayName("Adapter Id") : amended, DisplayInHex,
    description("Id that is globally unique to each instance 
    of each adapter. Using the address of the Adapter 
    Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), DisplayName("Session Digest Errors"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Session digest errors"): amended]
    uint32  SessionDigestErrorCount;
  [WmiDataId(3), DisplayName("Session Cxn Timeout Errors"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Session connection timeout
    error"): amended] 
    uint32  SessionConnectionTimeoutErrorCount;
  [WmiDataId(4), DisplayName("Session Format Errors"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Session format error"): amended]
    uint32  SessionFormatErrorCount;
  [WmiDataId(5),
    DisplayName("Sessions Failed"): amended, PerfDefault,
    CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Number of Sessions failed belonging to this 
    instance"): amended] 
    uint32  SessionFailureCount;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ InitiatorInstanceStatistics**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_initiatorinstancestatistics) 数据结构。

 

