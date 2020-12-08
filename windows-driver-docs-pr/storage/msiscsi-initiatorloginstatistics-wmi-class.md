---
title: MSiSCSI \_ INITIATORLOGINSTATISTICS WMI 类
description: MSiSCSI \_ INITIATORLOGINSTATISTICS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c40bb28a727626371541a0c3715ce0926f1c7d8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830967"
---
# <a name="msiscsi_initiatorloginstatistics-wmi-class"></a>MSiSCSI \_ INITIATORLOGINSTATISTICS WMI 类


## <span id="ddk_msiscsi_initiatorloginstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORLOGINSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI \_ INITIATORLOGINSTATISTICS WMI 类公开登录统计信息。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

MSiSCSI \_ InitiatorLoginStatistics 类是在 *Iscsiprf* 中定义的。

```cpp
class MSiSCSI_InitiatorLoginStatistics : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to 
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), DisplayName("Login Accept Responses"): 
    amended, PerfDefault, CounterType(0x00010000),
    //    PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of Login Accept Responses"): amended] 
    uint32  LoginAcceptRsps;
  [WmiDataId(3), DisplayName("Login Other Failed Responses") 
    : amended, CounterType(0x00010000),
    //    PERF_COUNTER_RAWCOUNT
    PerfDefault, DefaultScale(0), PerfDetail(100),
    read, Description("Count of Login other failed
    Responses"): amended] 
    uint32 LoginOtherFailRsps;
  [WmiDataId(4), DisplayName("Login Redirect Responses"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Login Redirect Responses"): 
    amended] 
    uint32 LoginRedirectRsps;
  [WmiDataId(5), DisplayName("Login Authentication Failed 
    Responses"): amended, PerfDefault,
    CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Login Authentication Failed 
    Responses"): amended] 
    uint32 LoginAuthFailRsps;
  [WmiDataId(6), DisplayName("Logins  Faiedl (Tar Auth)"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of the number of times a login is 
    aborted due to a target authentication failure"): 
    amended] 
    uint32 LoginAuthenticateFails;
  [WmiDataId(7), DisplayName("Login Negotiation Failed"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of the number of times login failed 
    due to negotiation failure with target"): amended] 
    uint32 LoginNegotiateFails;
  [WmiDataId(8), DisplayName("Logout Normal"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Logout command PDU with reason 
    code 0"): amended] 
    uint32 LogoutNormals;
  [WmiDataId(9), DisplayName("Logout Other Codes"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Logout command PDUs with status 
    code other than 0"): amended] 
    uint32 LogoutOtherCodes;
  [WmiDataId(10), DisplayName("Failed Logins"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("The object counts the number of times a 
    login attempt from this local initiator has failed"): 
    amended] 
    uint32 LoginFailures;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ InitiatorLoginStatistics**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_initiatorloginstatistics) 数据结构。

 

