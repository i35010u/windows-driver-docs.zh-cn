---
title: SM\_SendRPL 函数
description: SM\_SendRPL WMI 方法通过指示的端口将读取端口列表（RPL）命令发送到指定的目标端口。
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
ms.openlocfilehash: f7d6e399de3f03604080108621875c00a73ad541
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845456"
---
# <a name="sm_sendrpl-function"></a>SM\_SendRPL 函数


SM\_SendRPL WMI 方法通过指示的端口将读取端口列表（RPL）命令发送到指定的目标端口。

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
用于发送读取端口列表（RPL）命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRPL 的 PortWWN 成员中的微型端口驱动程序。

*AgentWWN*   
端口的全球名称（WWN），将查询该端口以获取 FC\_端口的端口列表。 有关 FC\_端口的定义，请参阅 T11 委员会的*光纤通道 HBA API*规范。 此信息将传送到 SM\_\_SendRPL 的 AgentWWN 成员中的微型端口驱动程序。

*AgentDomain*   
要查询其类型 FC\_端口的端口列表的域控制器的域名。 有关 FC\_端口的定义，请参阅 T11 委员会的*光纤通道 HBA API*规范。 此信息将传送到 SM\_SendRPL\_的代理中的微型端口驱动程序\_域成员。

*PortIndex*   
要返回 FC\_端口的端口列表中第一个端口的端口索引。 此信息将传送到 SM\_\_SendRPL 的 portIndex 成员中的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SendRPL\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalRespBufferSize*   
读取端口列表（RPL）命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRPL\_OUT 结构的 TotalRespBufferSize 成员中返回此信息。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRPL\_OUT 结构的 OutRespBufferSize 成员中返回此信息。

*RespBuffer*   
读取端口列表（RPL）命令的结果。 微型端口驱动程序在 SendRPL\_OUT 结构的 RespBuffer 成员中返回此信息。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_in)

[**SM\_SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_out)

 

 






