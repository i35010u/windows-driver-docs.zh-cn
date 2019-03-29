---
title: MS\_SM\_FabricAndDomainManagementMethods WMI 类
description: MS\_SM\_FabricAndDomainManagementMethods WMI 类
ms.assetid: dfd6afd3-0a0c-4620-b961-2235a91d8b17
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b107d42bcf379c6d01f952ecd4105877d0ae19ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575677"
---
# <a name="mssmfabricanddomainmanagementmethods-wmi-class"></a>MS\_SM\_FabricAndDomainManagementMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SM\_FabricAndDomainManagementMethods WMI 类向 WMI 客户端中提供光纤通道服务。 光纤通道服务定义 T11 委员会*光纤通道 HBA API*规范。 此 WMI 类都有无数据块。 因此，WMI 工具套件生成保存属于类的方法的参数数据结构，但它不会生成对应于类本身的结构。

每个方法都属于此类的 MOF 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

SM\_SendTEST

SM\_SendECHO

SM\_SendSMPPassThru

[**SM\_SendCTPassThru**](sm-sendctpassthru.md)

[**SM\_GetRNIDMgmtInfo**](sm-getrnidmgmtinfo.md)

[**SM\_SetRNIDMgmtInfo**](sm-setrnidmgmtinfo.md)

[**SM\_SendRNID**](sm-sendrnid.md)

[**SM\_SendRPL**](sm-sendrpl.md)

[**SM\_SendRPS**](sm-sendrps.md)

[**SM\_SendSRL**](sm-sendsrl.md)

[**SM\_SendLIRR**](sm-sendlirr.md)

[**SM\_SendRLS**](sm-sendrls.md)

MS\_SM\_FabricAndDomainManagementMethods 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SM_FabricAndDomainManagementMethods
{
    [key]
    string  InstanceName;
    boolean Active;

// new FC specific

    [Implemented, WmiMethodId(1)]
    void SM_SendTEST(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
                );

// new FC specific

    [Implemented, WmiMethodId(2)]
    void SM_SendECHO(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// new SAS specific

    [Implemented, WmiMethodId(3)]
    void SM_SendSMPPassThru(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(10)]
    void SM_SendCTPassThru(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(11)]
    void SM_GetRNIDMgmtInfo(
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] HBAFC3MgmtInfo MgmtInfo
                );

// old FC specific

    [Implemented, WmiMethodId(12)]
    void SM_SetRNIDMgmtInfo(
                [in ] HBAFC3MgmtInfo MgmtInfo,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
                );

// old FC specific

    [Implemented, WmiMethodId(13)]
    void SM_SendRNID(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  NodeIdDataFormat,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(14)]
    void SM_SendRPL(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 AgentWWN[8],
                [in ] uint32  AgentDomain,
                [in ] uint32  PortIndex,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(15)]
    void SM_SendRPS(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 AgentWWN[8],
                [in, HBAType("HBA_WWN")] uint8 ObjectWWN[8],
                [in ] uint32  AgentDomain,
                [in ] uint32  ObjectPortNumber,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(16)]
    void SM_SendSRL(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 WWN[8],
                [in ] uint32  Domain,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(17)]
    void SM_SendLIRR(
                [in, HBAType("HBA_WWN")] uint8 SourceWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint8   Function,
                [in ] uint8   Type,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(18)]
    void SM_SendRLS(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );
};
```

 

 





