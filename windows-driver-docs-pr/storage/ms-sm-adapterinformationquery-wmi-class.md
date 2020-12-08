---
title: MS \_ SM \_ AdapterInformationQuery WMI 类
description: MS \_ SM \_ AdapterInformationQuery WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f9fe1c6feeb9a2dc5a4538f65e36706e569a9c23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811543"
---
# <a name="ms_sm_adapterinformationquery-wmi-class"></a>MS \_ SM \_ AdapterInformationQuery WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ AdapterInformationQuery 类公开与 SAS 适配器关联的属性信息。

MS \_ SM \_ AdapterInformationQuery 类在 *Hbaapi* 中定义如下：

```cpp
class MS_SM_AdapterInformationQuery
{
    [key] 
    string  InstanceName;
    boolean Active;

    [Description ("Unique identifier for the adapter. This idenitifer must "
                  "be unique among all adapters. The same "
                  "value for the identifier must be used for the same adapter "
                  "in other classes that expose adapter information"),

  // WmiRefClass("MS_SM_ChannelAdapter"),  // ?? need a new ref class
     WmiRefProperty("UniqueAdapterId"),
     WmiDataId(1)
    ]
    uint64 UniqueAdapterId;             // CIM_FibreChannelAdapter REF
                                        // ?? need a new REF 

    [HBA_STATUS_QUALIFIERS, 
     WmiDataId(2)
    ]
    HBA_STATUS HBAStatus;

    [WmiDataId(3)]
    uint32 NumberOfPorts;   

    [WmiDataId(4)]
    uint32 VendorSpecificID;

    [
     cpp_quote("\n"
     "   //******************************************************************\n"
     "   //\n"
     "   //  The string type is variable length (up to MaxLen).              \n"
     "   //  Each string starts with a ushort that holds the strings length  \n"
     "   //  (in bytes) followed by the WCHARs that make up the string.      \n"
     "   //\n"
     "   //******************************************************************\n"
     "\n"),

     MaxLen(64), 
     WmiDataId(5)
    ]
    string Manufacturer;

    [MaxLen(64), WmiDataId(6)]
    string SerialNumber;

    [MaxLen(256), WmiDataId(7)]
    string Model;

    [MaxLen(256), WmiDataId(8)]
    string ModelDescription;

    [MaxLen(256), WmiDataId(9)]
    string HardwareVersion;

    [MaxLen(256), WmiDataId(10)]
    string DriverVersion;

    [MaxLen(256), WmiDataId(11)]
    string OptionROMVersion;

    [MaxLen(256), WmiDataId(12)]
    string FirmwareVersion;

    [MaxLen(256), WmiDataId(13)]
    string DriverName;

    [MaxLen(256), WmiDataId(14)]
    string HBASymbolicName;

    [MaxLen(256), WmiDataId(15)]
    string RedundantOptionROMVersion;

    [MaxLen(256), WmiDataId(16)]
    string RedundantFirmwareVersion;

    [MaxLen(256), WmiDataId(17)]
    string MfgDomain;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SM \_ AdapterInformationQuery**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_sm_adapterinformationquery)

没有与此 WMI 类相关联的方法。

 

