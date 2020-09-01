---
title: SendLIRR 函数
description: SendLIRR WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册 (LIRR) 命令。
ms.assetid: ca54161d-d5fe-4775-a38c-dfaf3fd8c00b
keywords:
- SendLIRR 函数存储设备
topic_type:
- apiref
api_name:
- SendLIRR
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3277a3b4b1d92cf45e3a45814f06e9638a3092f7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186871"
---
# <a name="sendlirr-function"></a>SendLIRR 函数


**SendLIRR** WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册 (LIRR) 命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendLIRR(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                SourceWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint8                                    Function,
   [in] uint8                                    Type,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**SendLIRR \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)结构的**HBAStatus**成员中返回此信息。

*SourceWWN*   
用于发送 LIRR 命令的本地端口的全球名称。 此信息将传送到结构[** \_ 中 SendLIRR**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)的**SourceWWN**成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称。 此信息将传送到结构[** \_ 中 SendLIRR**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)的**DestWWN**成员中的微型端口驱动程序。

*才能*   
标识要执行的注册函数的代码。 有关可分配给此成员的值的说明，请参阅 T11 委员会 *光纤通道组帧和信号* 规范。 此信息将传送到结构中[**SendLIRR \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)的**函数**成员的微型端口驱动程序。

*类别*   
请求其链接信息的设备类型。 有关可分配给此成员的值的说明，请参阅 T11 委员会 *光纤通道组帧和信号* 规范。 此信息将传送到结构中[**SendLIRR \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)的**函数**成员的微型端口驱动程序。

*TotalRspBufferSize*   
LIRR 命令的结果的大小（以字节为单位）。 微型端口驱动程序在[**SendLIRR \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)结构的**TotalRspBufferSize**成员中返回此信息。

*ActualRspBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在[**SendLIRR \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)结构的**ActualRspBufferSize**成员中返回此信息。

*RspBuffer*   
LIRR 命令的结果。 微型端口驱动程序在[**SendLIRR \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)结构的**RspBuffer**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
-------

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SendLIRR \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)

[**SendLIRR \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)

 

