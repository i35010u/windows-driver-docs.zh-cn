---
title: SM \_ SendRPS 函数
description: SM \_ SENDRPS WMI 方法将 (RPS) 请求的读取端口状态块发送到指定的端口或域控制器。
ms.assetid: a64983ef-c665-43db-ad29-0a6f14421ab8
keywords:
- SM_SendRPS 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendRPS
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c708a23da89660b6c34c37f2b67c6d0bcfaf3551
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184180"
---
# <a name="sm_sendrps-function"></a>SM \_ SendRPS 函数


SM \_ SENDRPS WMI 方法将 (RPS) 请求的读取端口状态块发送到指定的端口或域控制器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendRPS(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              AgentWWN[8],
   [in, HBAType("HBA_WWN")] uint8              ObjectWWN[8],
   [in] uint32                                 AgentDomain,
   [in] uint32                                 ObjectPortNumber,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
全球名称 (WWN) 用于发送 RPS 命令的本地端口。 此信息将传送到 SM SendRPS 结构中的 PortWWN 成员的微型端口驱动程序 \_ \_ 。

*AgentWWN*   
 (WWN) 的全球名称，将查询该端口以获取 ObjectWWN 所指示的端口状态。 此信息将传送到 SM SendRPS 结构中的 AgentWWN 成员的微型端口驱动程序 \_ \_ 。

*ObjectWWN*   
要为其返回端口状态的端口的全球名称 (WWN) 。 此信息将传送到 SM SendRPS 结构中的 ObjectWWN 成员的微型端口驱动程序 \_ \_ 。

*AgentDomain*   
要查询 ObjectWWN 指示的端口状态的域控制器的域名。 此信息将传送到 SM SendRPS 结构中的 AgentDomain 成员的微型端口驱动程序 \_ \_ 。

*ObjectPortNumber*   
要为其返回端口状态的端口的全球名称 (WWN) 。 此信息将传送到 SM SendRPS 结构中的 ObjectPortNumber 成员的微型端口驱动程序 \_ \_ 。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SendRPL OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*TotalRespBufferSize*   
RPS 命令结果的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendRPS OUT 结构的 TotalRespBufferSize 成员中返回此信息 \_ 。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendRPL OUT 结构的 OutRespBufferSize 成员中返回此信息 \_ 。

*RespBuffer*   
RPS 命令的结果。 微型端口驱动程序在 SM \_ SendRPS OUT 结构的 RespBuffer 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ FabricAndDomainManagementMethods WMI 类。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ SendRPS \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrps_out)

 

