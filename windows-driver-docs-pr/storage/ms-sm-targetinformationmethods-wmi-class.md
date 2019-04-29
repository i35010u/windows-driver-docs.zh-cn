---
title: MS\_SM\_TargetInformationMethods WMI 类
description: MS\_SM\_TargetInformationMethods WMI 类
ms.assetid: faedf8cf-d69f-4a4c-bc32-fd6df102d027
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bd96c34c5371473a99e4630594ff4cbdc27647a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361971"
---
# <a name="mssmtargetinformationmethods-wmi-class"></a>MS\_SM\_TargetInformationMethods WMI 类


WMI 客户端使用 MS\_SM\_TargetInformationMethods WMI 类，查询光纤通道协议 (FCP) 信息的 HBA 微型端口驱动程序。 FCP HBA 微型端口驱动程序定义有关 FCP 信息函数的部分中的 T11 委员会*光纤通道 HBA API*规范。 此 WMI 类都有无数据块。 因此，WMI 工具套件生成保存属于类的方法的参数数据结构，但它不会生成对应于类本身的结构。

每个方法都属于此类的 MOF 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

[**SM\_GetTargetMapping**](sm-gettargetmapping.md)

[**SM\_GetBindingCapability**](sm-getbindingcapability.md)

[**SM\_GetBindingSupport**](sm-getbindingsupport.md)

[**SM\_SetBindingSupport**](sm-setbindingsupport.md)

[**SM\_GetPersistentBinding**](sm-getpersistentbinding.md)

[**SM\_SetPersistentBinding**](sm-setpersistentbinding.md)

[**SM\_RemovePersistentBinding**](sm-removepersistentbinding.md)

[**SM\_GetLUNStatistics**](sm-getlunstatistics.md)

MS\_SM\_TargetInformationMethods 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SM_TargetInformationMethods
{
    [key]
    string  InstanceName;
    boolean Active;

    [Implemented, WmiMethodId(1)]
    void SM_GetTargetMapping(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 InEntryCount,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out] 
                 uint32 TotalEntryCount,
                [out] 
                 uint32 OutEntryCount,
                [out, WmiSizeIs("OutEntryCount")]
                 MS_SMHBA_SCSIENTRY Entry[]
                );

    [Implemented, WmiMethodId(2)]
    void SM_GetBindingCapability(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
                [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags
                );

    [Implemented, WmiMethodId(3)]
    void SM_GetBindingSupport(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out, HBAType("SMHBA_BIND_CAPABILITY")]
                 uint32 Flags
                );

    [Implemented, WmiMethodId(4)]
    void SM_SetBindingSupport(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("SMHBA_BIND_CAPABILITY")]
                 uint32 Flags,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus
                );

    [Implemented, WmiMethodId(5)]
    void SM_GetPersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 InEntryCount,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out]
                 uint32 TotalEntryCount,
                [out]
                 uint32 OutEntryCount,
                [out, WmiSizeIs("OutEntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[]
                );

    [Implemented, WmiMethodId(6)]
    void SM_SetPersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ] uint32 InEntryCount,
                [in, WmiSizeIs("InEntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out ] uint32 OutStatusCount,
                [out, WmiSizeIs("OutStatusCount")]
                 HBA_STATUS EntryStatus[]
                );

    [Implemented, WmiMethodId(7)]
    void SM_RemovePersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 EntryCount,
                [in, WmiSizeIs("EntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus
                );

    [Implemented, WmiMethodId(8)]
    void SM_GetLUNStatistics(
                [in, HBAType("HBA_SCSIID")]
                 HBAScsiID Lunit,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS") ]
                 MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
                );
};
```

 

 





