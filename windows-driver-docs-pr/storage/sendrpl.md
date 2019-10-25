---
title: SendRPL 函数
description: SendRPL WMI 方法通过所指示的端口将读取端口列表（RPL）命令发送到指定的目标端口。
ms.assetid: 3cf3dfe2-6ff9-431f-b6bf-66ef8dd77df3
keywords:
- SendRPL 函数存储设备
topic_type:
- apiref
api_name:
- SendRPL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 58460bbed809a64ea313cde127218e10f197bff8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832011"
---
# <a name="sendrpl-function"></a>SendRPL 函数


**SendRPL** WMI 方法通过所指示的端口将读取端口列表（RPL）命令发送到指定的目标端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRPL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                AgentWWN[8],
   [in] uint32                                   agent_domain,
   [in] uint32                                   portIndex,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)结构的**HBAStatus**成员中返回此信息。

*PortWWN*   
用于发送读取端口列表（RPL）命令的本地端口的全球名称。 此信息将传送到结构中[**SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)的**PortWWN**成员中的微型端口驱动程序。

*AgentWWN*   
端口的全球名称，将查询该端口以获取 FC\_端口的端口列表。 有关 FC\_端口的定义，请参阅 T11 委员会的*光纤通道 HBA API*规范。 此信息将传送到结构中[**SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)的**AgentWWN**成员中的微型端口驱动程序。

*代理\_域*   
要查询其类型 FC\_端口的端口列表的域控制器的域名。 有关 FC\_端口的定义，请参阅 T11 委员会的*光纤通道 HBA API*规范。 此信息将传送到[**SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)结构中的**代理\_域**成员中的微型端口驱动程序。

*portIndex*   
要返回 FC\_端口的端口列表中第一个端口的端口索引。 此信息将传送到结构中[**SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)的**portIndex**成员中的微型端口驱动程序。

*TotalRspBufferSize*   
读取端口列表（RPL）命令的结果大小（以字节为单位）。 微型端口驱动程序在[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)结构的**TotalRspBufferSize**成员中返回此信息。

*ActualRspBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)结构的**ActualRspBufferSize**成员中返回此信息。

*RspBuffer*   
读取端口列表（RPL）命令的结果。 微型端口驱动程序在[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)结构的**RspBuffer**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAADAPTERMETHODS WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">Hbapiwmi （包括 Hbapiwmi、Hbaapi 或 Hbaapi）。</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)

[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)

 

 






