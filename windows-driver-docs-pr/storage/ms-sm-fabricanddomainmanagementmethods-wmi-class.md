---
title: MS \_ SM \_ FabricAndDomainManagementMethods WMI 类
description: MS \_ SM \_ FabricAndDomainManagementMethods WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d926d05f0746818fd9969d50b57177306815853b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811531"
---
# <a name="ms_sm_fabricanddomainmanagementmethods-wmi-class"></a>MS \_ SM \_ FabricAndDomainManagementMethods WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ FabricAndDomainManagementMethods wmi 类向 wmi 客户端提供光纤通道服务。 光纤通道服务由 T11 委员会 *光纤通道 HBA API* 规范定义。 此 WMI 类没有数据块。 因此，WMI 工具套件会生成包含属于类的方法的参数数据的结构，但不会生成对应于类本身的结构。

此类的每个方法的 MOF 语法在方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

SM \_ SendTEST

SM \_ SendECHO

SM \_ SendSMPPassThru

[**SM \_ SendCTPassThru**](sm-sendctpassthru.md)

[**SM \_ GetRNIDMgmtInfo**](sm-getrnidmgmtinfo.md)

[**SM \_ SetRNIDMgmtInfo**](sm-setrnidmgmtinfo.md)

[**SM \_ SendRNID**](sm-sendrnid.md)

[**SM \_ SendRPL**](sm-sendrpl.md)

[**SM \_ SendRPS**](sm-sendrps.md)

[**SM \_ SendSRL**](sm-sendsrl.md)

[**SM \_ SendLIRR**](sm-sendlirr.md)

[**SM \_ SendRLS**](sm-sendrls.md)

MS \_ SM \_ FabricAndDomainManagementMethods 类在 *Hbaapi* 中定义如下：

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

 

 





