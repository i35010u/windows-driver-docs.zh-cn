---
title: MS\_SM\_ScsiInformationMethods WMI 类
description: MS\_SM\_ScsiInformationMethods WMI 类
ms.assetid: 13e70e48-5364-4a63-8a83-d5ac02c8d17f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb0b83b622bdd965adb9e0cecd72ee72dae959f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367477"
---
# <a name="mssmscsiinformationmethods-wmi-class"></a>MS\_SM\_ScsiInformationMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SM\_ScsiInformationMethods WMI 类发送 SCSI 命令。 此 WMI 类都有无数据块。 因此，WMI 工具套件生成保存属于类的方法的参数数据结构，但它不会生成对应于类本身的结构。

每个方法都属于此类的 MOF 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

[**SM\_ScsiInquiry**](sm-scsiinquiry.md)

[**SM\_ScsiReportLuns**](sm-scsireportluns.md)

[**SM\_ScsiReadCapacity**](sm-scsireadcapacity.md)

MS\_SM\_ScsiInformationMethods 类定义，如下所示在*Hbaapi.mof*:

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

 

 





