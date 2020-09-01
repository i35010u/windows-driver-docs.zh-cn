---
title: SM \_ SendRPL 函数
description: SM \_ SENDRPL WMI 方法通过显示的端口将读取端口列表 (RPL) 命令发送到指定的目标端口。
ms.assetid: 9297d5eb-f8c4-48f3-8536-a94c66917e66
keywords:
- SM_SendRPL 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendRPL
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4b3e76c8c406ca6bf99bd40b7d0a4b2a6ba95c1b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187527"
---
# <a name="sm_sendrpl-function"></a>SM \_ SendRPL 函数


SM \_ SENDRPL WMI 方法通过显示的端口将读取端口列表 (RPL) 命令发送到指定的目标端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendRPL(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              AgentWWN[8],
   [in] uint32                                 AgentDomain,
   [in] uint32                                 PortIndex,
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
为本地端口 (WWN) 提供全球名称，通过该端口，可通过该端口发送读取端口列表 (RPL) 命令。 此信息将传送到 SM SendRPL 结构中的 PortWWN 成员的微型端口驱动程序 \_ \_ 。

*AgentWWN*   
全球名称 (WWN) ，将查询该端口以获取 FC 端口类型端口的列表 \_ 。 有关 FC 端口的定义 \_ ，请参阅 T11 委员会 *光纤通道 HBA API* 规范。 此信息将传送到 SM SendRPL 结构中的 AgentWWN 成员的微型端口驱动程序 \_ \_ 。

*AgentDomain*   
要查询其类型为 FC 端口的端口列表的域控制器的域名 \_ 。 有关 FC 端口的定义 \_ ，请参阅 T11 委员会 *光纤通道 HBA API* 规范。 此信息将传送到 SM SendRPL 的 agent 域成员中的微型端口驱动程序 \_ \_ \_ 。

*PortIndex*   
要返回的 FC 端口类型的端口列表中第一个端口的端口索引 \_ 。 此信息将传送到 SM SendRPL 结构中的 portIndex 成员的微型端口驱动程序 \_ \_ 。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SendRPL OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*TotalRespBufferSize*   
读取端口列表的结果大小（以字节为单位） (RPL) 命令。 微型端口驱动程序在 SM \_ SendRPL OUT 结构的 TotalRespBufferSize 成员中返回此信息 \_ 。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendRPL OUT 结构的 OutRespBufferSize 成员中返回此信息 \_ 。

*RespBuffer*   
读取端口列表 (RPL) 命令的结果。 微型端口驱动程序在 SendRPL OUT 结构的 RespBuffer 成员中返回此信息 \_ 。

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

[**SM \_ SendRPL \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_in)

[**SM \_ SendRPL \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_out)

 

