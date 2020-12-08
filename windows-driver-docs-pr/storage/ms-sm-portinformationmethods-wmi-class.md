---
title: MS \_ SM \_ PortInformationMethods WMI 类
description: MS \_ SM \_ PortInformationMethods WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4392a1caecf792187e0d85e911ef6ff43191a93f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811515"
---
# <a name="ms_sm_portinformationmethods-wmi-class"></a>MS \_ SM \_ PortInformationMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ PortInformationMethods 类来查询端口属性。

MS \_ SM \_ PortInformationMethods 类在 *Hbaapi* 中定义如下：

```cpp
class MS_SM_PortInformationMethods
{
    [key]
    string  InstanceName;
    boolean Active;

    [Implemented, WmiMethodId(1)]
    void SM_GetPortType(
                [in ] 
                 uint32  PortIndex,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBA_PORTTYPE_QUALIFIERS ]
                 uint32  PortType
                );

    [Implemented, WmiMethodId(2)]
    void SM_GetAdapterPortAttributes(
                [in ] 
                 uint32  PortIndex,
                [in,
                 cpp_quote("#define SM_PORT_SPECIFIC_ATTRIBUTES_MAXSIZE "
                           " max(sizeof(MS_SMHBA_FC_Port), "
                           " sizeof(MS_SMHBA_SAS_Port))")
                ]
                 uint32  PortSpecificAttributesMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] 
                 HBA_STATUS  HBAStatus,
                [out, HBAType("MS_SMHBA_PORTATTRIBUTES") ] 
                 MS_SMHBA_PORTATTRIBUTES  PortAttributes
                );

    [Implemented, WmiMethodId(3)]
    void SM_GetDiscoveredPortAttributes(
                [in ] uint32  PortIndex,
                [in ] uint32  DiscoveredPortIndex,
                [in ] uint32  PortSpecificAttributesMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_PORTATTRIBUTES") ]
                 MS_SMHBA_PORTATTRIBUTES PortAttributes
                );

    [Implemented, WmiMethodId(4)]
    void SM_GetPortAttributesByWWN(
                [in, HBAType("HBA_WWN")] uint8  PortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 PortSpecificAttributesMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_PORTATTRIBUTES") ]
                 MS_SMHBA_PORTATTRIBUTES PortAttributes
                );

    [Implemented, WmiMethodId(5)]
    void SM_GetProtocolStatistics(
                [in ] uint32  PortIndex,
                [in ] uint32  ProtocolType,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS") ]
                 MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
                );

    [Implemented, 
     Description("Typical counters SMHBA_SASPHYSTATISTICS (9 counters) or"
                 " MSFC_HBAPortStatistics (15 counters)"),
     WmiMethodId(6)
    ]
    void SM_GetPhyStatistics(
                [in ] uint32  PortIndex,
                [in ] uint32  PhyIndex,
                [in ] uint32  InNumOfPhyCounters,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out] uint32  TotalNumOfPhyCounters, 
                [out] uint32  OutNumOfPhyCounters, 
                [out, WmiSizeIs("OutNumOfPhyCounters")]
                 sint64 PhyCounter[]
                );

    [Implemented, WmiMethodId(7)]
    void SM_GetFCPhyAttributes(
                [in ] uint32  PortIndex,
                [in ] uint32  PhyIndex,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_FC_PHY") ]
                 MS_SMHBA_FC_PHY PhyType
                );

    [Implemented, WmiMethodId(8)]
    void SM_GetSASPhyAttributes(
                [in ] uint32  PortIndex,
                [in ] uint32  PhyIndex,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_SAS_PHY") ]
                 MS_SMHBA_SAS_PHY PhyType
                );

    [Implemented, WmiMethodId(10)]
    void SM_RefreshInformation();
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

MS \_ SM \_ PortInformationMethods

没有与此 WMI 类相关联的方法。

 

 





