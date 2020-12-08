---
title: MS \_ SM \_ TargetInformationMethods WMI 类
description: MS \_ SM \_ TargetInformationMethods WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bd3b7c3a9e36b21d14bc6032f8466cf950cba815
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811511"
---
# <a name="ms_sm_targetinformationmethods-wmi-class"></a>MS \_ SM \_ TargetInformationMethods WMI 类


WMI 客户端使用 MS \_ SM \_ TargetInformationMethods WMI 类来查询适用于光纤通道协议的 HBA 微型端口驱动程序 (FCP) 信息。 适用于 FCP 的 HBA 微型端口驱动程序在 T11 委员会 *光纤通道 HBA API* 规范中有关 Fcp 信息函数的部分中定义。 此 WMI 类没有数据块。 因此，WMI 工具套件会生成包含属于类的方法的参数数据的结构，但不会生成对应于类本身的结构。

此类的每个方法的 MOF 语法在方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

[**SM \_ GetTargetMapping**](sm-gettargetmapping.md)

[**SM \_ GetBindingCapability**](sm-getbindingcapability.md)

[**SM \_ GetBindingSupport**](sm-getbindingsupport.md)

[**SM \_ SetBindingSupport**](sm-setbindingsupport.md)

[**SM \_ GetPersistentBinding**](sm-getpersistentbinding.md)

[**SM \_ SetPersistentBinding**](sm-setpersistentbinding.md)

[**SM \_ RemovePersistentBinding**](sm-removepersistentbinding.md)

[**SM \_ GetLUNStatistics**](sm-getlunstatistics.md)

MS \_ SM \_ TargetInformationMethods 类在 *Hbaapi* 中定义如下：

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

 

 





