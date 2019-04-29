---
title: WMI 类示例
description: WMI 类示例
ms.assetid: 5b0ef39a-32bd-4f62-ad8f-fdab74409294
keywords:
- WDK WMI 类
- WMI WDK 内核类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2933c5a30884e963066789a5e5013a5809918ee0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380929"
---
# <a name="wmi-class-examples"></a>WMI 类示例





以下示例演示从架构的串行端口驱动程序的类定义。 请注意， **guid**在这些示例中所示的值是占位符。 每个类定义必须由 guidgen.exe 或 uuidgen.exe （这包括在 Microsoft Windows SDK 中） 生成的唯一 GUID。

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

下面是上一示例中所示的嵌入类的类定义。 请注意，此类不包含**InstanceName**或**Active**项。

```cpp
// Example of an embedded class 
[WMI, guid("xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"),
class Vendor_XmitDescriptor {
    [read, WmiDataId(1)] int32 DestinationIndex;
    [read, WmiDataId(2)] int32 DestinationTarget;
}
```

下面是一个事件块的类定义。 类派生自**WmiEvent**。

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

 

 




