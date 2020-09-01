---
title: SM \_ SendLIRR 函数
description: SM \_ SENDLIRR WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册 (LIRR) 命令。
ms.assetid: 52564ec3-4a42-4df0-b89f-2a8415404172
keywords:
- SM_SendLIRR 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendLIRR
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b3e8998358bf89e20682b09ae51822c0a1e67f8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183827"
---
# <a name="sm_sendlirr-function"></a>SM \_ SendLIRR 函数


SM \_ SENDLIRR WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册 (LIRR) 命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendLIRR(
   [in, HBAType("HBA_WWN")]                    SourceWWN[8],
   [in, HBAType("HBA_WWN")]                    DestWWN[8],
   [in] uint8                                  Function,
   [in] uint8                                  Type,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>参数
----------

*SourceWWN*   
用于发送 LIRR 命令的本地端口的全球名称 (WWN) 。 此信息将传送到 SM SendLIRR 结构中的 SourceWWN 成员的微型端口驱动程序 \_ \_ 。

*DestWWN*   
针对目标端口 (WWN) 的全球名称。 此信息将传送到 SM SendLIRR 结构中的 DestWWN 成员的微型端口驱动程序 \_ \_ 。

*才能*   
标识要执行的注册函数的代码。 有关可分配给此成员的值的说明，请参阅 T11 委员会光纤通道组帧和信号规范。 此信息将传送到 SM SendLIRR 的函数成员的微型端口驱动程序 \_ \_ 。

*类别*   
请求其链接信息的设备类型。 有关可分配给此成员的值的说明，请参阅 T11 委员会 *光纤通道组帧和信号* 规范。 此信息将传送到 SM SendLIRR 的函数成员的微型端口驱动程序 \_ \_ 。

*InRespBufferMaxSize*   
响应缓冲区的最大大小（以字节为单位）。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ SendLIRR OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*TotalRespBufferSize*   
LIRR 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendLIRR OUT 结构的 TotalRespBufferSize 成员中返回此信息 \_ 。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendLIRR OUT 结构的 OutRespBufferSize 成员中返回此信息 \_ 。

*RespBuffer*   
LIRR 命令的结果。 微型端口驱动程序在 SM \_ SendLIRR OUT 结构的 RespBuffer 成员中返回此信息 \_ 。

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

[**SM \_ SendLIRR \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendlirr_out)

 

