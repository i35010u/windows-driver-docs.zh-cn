---
title: MSiSCSI \_ NICPERFORMANCE WMI 类
description: MSiSCSI \_ NICPERFORMANCE WMI 类
ms.assetid: e5894b20-8ea7-46ec-9960-3d9891b06ac4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: faf3baa96208163d747fae1f186517a95eaaed17
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190409"
---
# <a name="msiscsi_nicperformance-wmi-class"></a>MSiSCSI \_ NICPERFORMANCE WMI 类


## <span id="ddk_msiscsi_nicperformance_wmi_class_kr"></span><span id="DDK_MSISCSI_NICPERFORMANCE_WMI_CLASS_KR"></span>


MSiSCSI \_ NICPERFORMANCE WMI 类 (NIC) 端口公开网络接口卡的性能统计信息。 注册此类的微型端口驱动程序应为适配器上的每个端口创建类的一个实例。

发起方应 \_ 为适配器上的每个以太网端口实现一个 MSiSCSI NICPerformance 类的实例，并为该端口注册该类的每个实例 (PDO) 的特定物理设备对象的名称。

MSiSCSI \_ NICPerformance 类是在 *Iscsiprf*中定义的。

```cpp
class MSiSCSI_NICPerformance : Win32_PerfRawData {
  [key] string  InstanceName;
  boolean  Active;
  [read, WmiDataId(1), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second transmitted via Ethernet port") : 
    amended] 
    uint32  BytesTransmitted;
  [read, WmiDataId(2), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second received via Ethernet port") : amended] 
    uint32  BytesReceived;
  [read, WmiDataId(3), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second transmitted via Ethernet port") :
    amended] 
    uint32  PDUTransmitted;
  [read, WmiDataId(4), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second received via Ethernet port") : amended]
    uint32  PDUReceived;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ NICPerformance**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_nicperformance) 数据结构。

 

