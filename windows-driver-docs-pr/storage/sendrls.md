---
title: SendRLS 函数
description: SendRLS WMI 方法通过指定的远程端口将读取链接错误状态块发送 (RLS) ，以检索与远程端口关联的链接错误状态块。
keywords:
- SendRLS 函数存储设备
topic_type:
- apiref
api_name:
- SendRLS
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c3c306df84a3e58b661b543be023f5dde71e0d6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839379"
---
# <a name="sendrls-function"></a>SendRLS 函数


**SendRLS** WMI 方法通过指定的远程端口将读取链接错误状态块发送 (RLS) ，以检索与远程端口关联的链接错误状态块。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRLS(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**SendRLS \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)结构的 **HBAStatus** 成员中返回此信息。

*PortWWN*   
用于发送 RLS 命令的本地端口的全球名称。 此信息将传送到结构 [**\_ 中 SendRLS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)的 **PortWWN** 成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称。 此信息将传送到结构 [**\_ 中 SendRLS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)的 **DestWWN** 成员中的微型端口驱动程序。

*TotalRspBufferSize*   
RLS 命令结果的大小（以字节为单位）。 微型端口驱动程序在 [**SendRLS \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)结构的 **TotalRspBufferSize** 成员中返回此信息。

*ActualRspBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 [**SendRLS \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)结构的 **ActualRspBufferSize** 成员中返回此信息。

*RspBuffer*   
RLS 命令的结果。 微型端口驱动程序在 [**SendRLS \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)结构的 **RspBuffer** 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
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
<td align="left"><p>标头</p></td>
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

[**SendRLS \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)

[**SendRLS \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)

 

