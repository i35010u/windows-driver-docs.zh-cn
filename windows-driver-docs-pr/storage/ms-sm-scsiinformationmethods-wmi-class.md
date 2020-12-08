---
title: MS \_ SM \_ ScsiInformationMethods WMI 类
description: MS \_ SM \_ ScsiInformationMethods WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 617d0e4f99209401d75b16bf459c9e2980c83b35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811513"
---
# <a name="ms_sm_scsiinformationmethods-wmi-class"></a>MS \_ SM \_ ScsiInformationMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ ScsiInformationMethods WMI 类发送 SCSI 命令。 此 WMI 类没有数据块。 因此，WMI 工具套件会生成包含属于类的方法的参数数据的结构，但不会生成对应于类本身的结构。

此类的每个方法的 MOF 语法在方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

[**SM \_ ScsiInquiry**](sm-scsiinquiry.md)

[**SM \_ ScsiReportLuns**](sm-scsireportluns.md)

[**SM \_ ScsiReadCapacity**](sm-scsireadcapacity.md)

MS \_ SM \_ ScsiInformationMethods 类在 *Hbaapi* 中定义如下：

```cpp
class MS_SM_ScsiInformationMethods
{
    [key]
    string  InstanceName;
    boolean Active;

    [Implemented, WmiMethodId(1)]
    void SM_ScsiInquiry(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("HBA_SCSILUN")]
                 uint64 SmhbaLUN,
                [in ]
                 uint8  Cdb[6],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8 RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8 SenseBuffer[]
                );

    [Implemented, WmiMethodId(2)]
    void SM_ScsiReportLuns(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint8  Cdb[12],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 TotalRespBufferSize,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8 RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8 SenseBuffer[]
                );
 
    [Implemented, WmiMethodId(3)]
    void SM_ScsiReadCapacity(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("HBA_SCSILUN")]
                 uint64 SmhbaLUN,
                [in ]
                 uint8  Cdb[16],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8  RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8  SenseBuffer[]
                );
};
```

 

 





