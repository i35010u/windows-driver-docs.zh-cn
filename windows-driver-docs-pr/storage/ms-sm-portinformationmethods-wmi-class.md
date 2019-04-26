---
title: MS\_SM\_PortInformationMethods WMI 类
description: MS\_SM\_PortInformationMethods WMI 类
ms.assetid: 5bf44288-7e1f-48e6-aa02-1e706b73f046
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60bc3f8955c4891639459b1a15698956850d64d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329827"
---
# <a name="mssmportinformationmethods-wmi-class"></a>MS\_SM\_PortInformationMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SM\_PortInformationMethods 类查询端口属性。

MS\_SM\_PortInformationMethods 类定义，如下所示在*Hbaapi.mof*:

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

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

MS\_SM\_PortInformationMethods

没有与此 WMI 类相关联的方法。

 

 





