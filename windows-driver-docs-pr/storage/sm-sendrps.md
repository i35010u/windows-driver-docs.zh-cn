---
title: SM\_SendRPS 函数
description: SM\_SendRPS WMI 方法将读取端口状态块（RPS）请求发送到指定的端口或域控制器。
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
ms.openlocfilehash: 6f44a495c4438cd39bd2c3f0570f96be10d82553
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845453"
---
# <a name="sm_sendrps-function"></a>SM\_SendRPS 函数


SM\_SendRPS WMI 方法将读取端口状态块（RPS）请求发送到指定的端口或域控制器。

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
用于发送 RPS 命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRPS 的 PortWWN 成员中的微型端口驱动程序。

*AgentWWN*   
端口的全球名称（WWN），将在该端口上查询 ObjectWWN 所指示的端口状态。 此信息将传送到 SM\_\_SendRPS 的 AgentWWN 成员中的微型端口驱动程序。

*ObjectWWN*   
要为其返回端口状态的端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRPS 的 ObjectWWN 成员中的微型端口驱动程序。

*AgentDomain*   
要查询 ObjectWWN 指示的端口状态的域控制器的域名。 此信息将传送到 SM\_\_SendRPS 的 AgentDomain 成员中的微型端口驱动程序。

*ObjectPortNumber*   
要为其返回端口状态的端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRPS 的 ObjectPortNumber 成员中的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SendRPL\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalRespBufferSize*   
RPS 命令结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRPS\_OUT 结构的 TotalRespBufferSize 成员中返回此信息。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRPL\_OUT 结构的 OutRespBufferSize 成员中返回此信息。

*RespBuffer*   
RPS 命令的结果。 微型端口驱动程序在 SM\_SendRPS\_OUT 结构的 RespBuffer 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_FabricAndDomainManagementMethods WMI 类。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SendRPS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrps_out)

 

 






