---
title: MSiSCSI\_NICPerformance WMI 类
description: MSiSCSI\_NICPerformance WMI 类
ms.assetid: e5894b20-8ea7-46ec-9960-3d9891b06ac4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9eb630d3ae93d32e7695ab5bdc65d5df0735b324
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387456"
---
# <a name="msiscsinicperformance-wmi-class"></a>MSiSCSI\_NICPerformance WMI 类


## <span id="ddk_msiscsi_nicperformance_wmi_class_kr"></span><span id="DDK_MSISCSI_NICPERFORMANCE_WMI_CLASS_KR"></span>


MSiSCSI\_NICPerformance WMI 类公开的网络接口卡 (NIC) 端口的性能统计信息。 注册此类的微型端口驱动程序应在适配器上创建的类的每个端口的一个实例。

发起方应实现一个实例 MSiSCSI\_NICPerformance 类为每个以太网端口在适配器上和注册端口的特定物理设备对象 (PDO) 的类名称的每个实例。

MSiSCSI\_NICPerformance 类中定义*Iscsiprf.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_NICPerformance** ](https://msdn.microsoft.com/library/windows/hardware/ff563087)数据结构。

 

 





