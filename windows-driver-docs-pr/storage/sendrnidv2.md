---
title: SendRNIDV2 函数
description: SendRNIDV2 WMI 方法向指定的端口发送版本 2 RNID 命令。
keywords:
- SendRNIDV2 函数存储设备
topic_type:
- apiref
api_name:
- SendRNIDV2
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 904ceb788d7f51be5342e73bdebd121beb844ef1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804389"
---
# <a name="sendrnidv2-function"></a>SendRNIDV2 函数


**SendRNIDV2** WMI 方法向指定的端口发送版本 2 RNID 命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRNIDV2(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint32                                   DestFCID,
   [in] uint32                                   NodeIdDataFormat,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**SendRNIDV2 \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构的 **HBAStatus** 成员中返回此信息。

*PortWWN*   
用于发送版本 2 RNID 命令的本地端口的全球名称。 此信息将传送到结构 [**\_ 中 SendRNIDV2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)的 **PortWWN** 成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称。 此信息将传送到结构 [**\_ 中 SendRNIDV2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)的 **DestWWN** 成员中的微型端口驱动程序。

*DestFCID*   
目标端口的地址标识符。 此信息将传送到结构 [**\_ 中 SendRNIDV2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)的 **DestFCID** 成员中的微型端口驱动程序。

*NodeIdDataFormat*   
节点标识数据格式。 有关此成员可以具有的值的说明，请参阅 T11 委员会 *光纤通道 HBA API* 规范。 此信息将传送到结构 [**\_ 中 SendRNIDV2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)的 **NodeIdDataFormat** 成员中的微型端口驱动程序。

*TotalRspBufferSize*   
版本 2 RNID 命令结果的大小（以字节为单位）。 微型端口驱动程序在 [**SendRNIDV2 \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构的 **TotalRspBufferSize** 成员中返回此信息。

*ActualRspBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 [**SendRNIDV2 \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构的 **ActualRspBufferSize** 成员中返回此信息。

*RspBuffer*   
版本 2 RNID 命令的结果。 微型端口驱动程序在 [**SendRNIDV2 \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构的 **RspBuffer** 成员中返回此信息。

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

[**SendRNIDV2 \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)

[**SendRNIDV2 \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)

 

