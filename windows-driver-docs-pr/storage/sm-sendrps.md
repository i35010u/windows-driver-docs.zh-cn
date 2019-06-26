---
title: SM\_SendRPS 函数
description: SM\_SendRPS WMI 方法将读取的端口状态块 (RPS) 请求发送到指定的端口或域控制器。
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
ms.openlocfilehash: 2030111598ad5cef739af4a1f341c6071f3a462a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354898"
---
# <a name="smsendrps-function"></a>SM\_SendRPS 函数


SM\_SendRPS WMI 方法将读取的端口状态块 (RPS) 请求发送到指定的端口或域控制器。

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

<a name="parameters"></a>Parameters
----------

*PortWWN*   
通过其发送的 RPS 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM 端口全球通用名称成员中的微型端口驱动程序\_SendRPS\_结构中。

*AgentWWN*   
若要查询的 ObjectWWN 指示该端口的状态的端口全球通用名称 (WWN)。 此信息传递到 SM AgentWWN 成员中的微型端口驱动程序\_SendRPS\_结构中。

*ObjectWWN*   
全球通用名称 (WWN) 的端口的端口为返回状态。 此信息传递到 SM ObjectWWN 成员中的微型端口驱动程序\_SendRPS\_结构中。

*AgentDomain*   
要查询由 ObjectWWN 指示该端口的状态的域控制器的域数。 此信息传递到 SM AgentDomain 成员中的微型端口驱动程序\_SendRPS\_结构中。

*ObjectPortNumber*   
全球通用名称 (WWN) 的端口的端口为返回状态。 此信息传递到 SM ObjectPortNumber 成员中的微型端口驱动程序\_SendRPS\_结构中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 SendRPL 在 HBAStatus 成员中返回此信息\_结构。

*TotalRespBufferSize*   
以字节为单位，RPS 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRespBufferSize 成员\_SendRPS\_结构。

*OutRespBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM OutRespBufferSize 成员\_SendRPL\_结构。

*RespBuffer*   
RPS 命令的结果。 微型端口驱动程序返回此信息在 SM RespBuffer 成员\_SendRPS\_结构。

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
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SendRPS\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_sendrps_out)

 

 






