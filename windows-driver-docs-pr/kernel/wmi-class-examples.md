---
title: WMI 类示例
description: WMI 类示例
keywords:
- 类 WDK WMI
- WMI WDK 内核，类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e03ec51d8b7beb2e10661d26ddd201e6fb85ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782683"
---
# <a name="wmi-class-examples"></a>WMI 类示例





以下示例显示了串行端口驱动程序的架构中的类定义。 请注意，这些示例中所示的 **guid** 值为占位符。 每个类定义必须具有由 guidgen.exe 或 uuidgen.exe (生成的唯一 GUID，包含在 Microsoft Windows SDK) 中。

```cpp
// Standard class for reporting serial port information
// Class qualifiers 
[WMI, guid("xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"),
Dynamic, Provider("WMIProv"),
WmiExpense(1),
Locale("MS\\0x409"),
Description("Description of class"]
 
//Class name 
class Vendor_SerialInfo {
 
//Required items 
    [key, read] 
     string InstanceName;
    [read]
     boolean Active;
 
// Bytes sent on port
// Property qualifiers 
    [read,
     WmiDataId(1),
     WmiScale(0),
     WmiComplexity(1),
     WmiVolatility(1000)]
     Description("Description of property")]
// Data item 
     uint64 BytesSent;
 
// Bytes received on port
    [read,
     write,
     WmiDataId(2),
     WmiScale(0), 
     WmiVolatility(1000)]
     uint64 BytesReceived;
 
// Who owns the port 
    [read,
     WmiDataId(4),
     WmiScale(0),              
     WmiVolatility(60000)] 
    string Owner;
 
// Status bit array
    [read, write,
     WmiDataId(3),
     WmiScale(0)]
     byte Status[16];
 
//The number of items in the XmitBufferSize array
    [read,
     WmiDataId(5),
     WmiScale(0),
     WmiComplexity(1),
     WmiVolatility(1000)]
     uint32 XmitDescriptorCount;       
 
//Array of XmitDescriptor classes
    [read,
     WmiDataId(6),
     WmiSizeIs("XmitDescriptorCount"),
     WmiScale(0),
     WmiComplexity(1),
     WmiVolatility(1000)]
    Vendor_XmitDescriptor XmitBufferSize[];
}
```

下面是前面的示例中所示的嵌入类的类定义。 请注意，此类不包含 **InstanceName** 或 **活动** 项。

```cpp
// Example of an embedded class 
[WMI, guid("xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"),
class Vendor_XmitDescriptor {
    [read, WmiDataId(1)] int32 DestinationIndex;
    [read, WmiDataId(2)] int32 DestinationTarget;
}
```

下面是事件块的类定义。 该类派生自 **register-wmievent**。

```cpp
// Example of an event
[WMI, Dynamic, Provider("WMIProv"),
guid("{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"),
locale("MS\\0x409"),
WmiExpense(1),
Description("Notify Toaster Arrival")]
class ToasterNotifyDeviceArrival : WMIEvent
{
    [key, read]
    string      InstanceName;

    [read]
    boolean           Active;

    [read,
     Description("Device Model Name"),
     WmiDataId(1)]    string     ModelName;
};
```

 

 




