---
title: MSiSCSI\_ConnectionStatistics WMI 类
description: MSiSCSI\_ConnectionStatistics WMI 类
ms.assetid: f12dfa6a-0999-40a3-9e15-bb65dc086911
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb34209bb0bcd75876c452a71aac64dcac864873
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534890"
---
# <a name="msiscsiconnectionstatistics-wmi-class"></a>MSiSCSI\_ConnectionStatistics WMI 类


## <span id="ddk_msiscsi_connectionstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_CONNECTIONSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI\_ConnectionStatistics WMI 类公开连接统计信息。 此类 Iscsiprf.mof 中定义，如下所示。

```cpp
class MSiSCSI_ConnectionStatistics : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), WmiVersion(1), 
    cpp_quote(
    "\n    //Text-based identifier for this Initiator that 
    is globally unique.\n"
    "    //The Initiator Name is independent of the location 
    of the initiator.\n"),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  iSCSIName;
  [read, WmiDataId(2), WmiVersion(1), Description("The iSCSI 
    connection ID for this connection instance."): amended] 
    uint16  CID; //session wide namespace
  [read, WmiDataId(3), Description("A uniquely generated 
    session ID used only internally.  Do not mix this with 
    ISID or SSID"): amended,
    cpp_quote(
    "\n    //A uniquely generated session ID used only 
    internally.  Do not mix this with ISID or SSID\n"),
    WmiVersion(1)] 
    uint64  USID;
  [WmiDataId(4), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to 
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(5), DisplayName("Bytes Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes sent over this 
    connection"): amended] 
    uint64  BytesSent;
  [WmiDataId(6), DisplayName("Bytes Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes received over this 
    connection"): amended] 
    uint64  BytesReceived;
  [WmiDataId(7), DisplayName("PDUs Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of  PDU Commands Sent over this 
    connection"): amended] 
    uint64  PDUCommandsSent;
  [WmiDataId(8), DisplayName("PDUs Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of PDUResponses received over 
    this connection"): amended] 
    uint64  PDUResponsesReceived;
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_ConnectionStatistics** ](https://msdn.microsoft.com/library/windows/hardware/ff562986)数据结构。

发起程序必须注册 MSiSCSI\_ConnectionStatistics WMI 类具有以下目标实例名称：

```cpp
targetname_#:#
```

第一个数字符号 (\#) 是中的值**USID**的成员[ **MSiSCSI\_ConnectionStatistics** ](https://msdn.microsoft.com/library/windows/hardware/ff562986)结构，第二个数字符号 (\#) 是中的值**CID**此类的成员。

 

 





