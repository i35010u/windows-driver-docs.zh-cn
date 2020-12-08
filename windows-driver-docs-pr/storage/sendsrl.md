---
title: SendSRL 函数
description: SendSRL WMI 方法通过指定的端口将扫描远程循环 (SRL) 命令发送到指定的域控制器。
keywords:
- SendSRL 函数存储设备
topic_type:
- apiref
api_name:
- SendSRL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ca9b590266816a346d7381ac91ced3002e71228b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792575"
---
# <a name="sendsrl-function"></a>SendSRL 函数


**SendSRL** WMI 方法通过指定的端口将扫描远程循环 (SRL) 命令发送到指定的域控制器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendSRL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                WWN[8],
   [in] uint32                                   Domain,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**SendSRL \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构的 **HBAStatus** 成员中返回此信息。

*PortWWN*   
用于发送 SRL 命令的本地端口的全球名称。 此信息将传送到结构中 SendSRL 的 **PortWWN** 成员中的微型端口驱动程序 \_ 。

*WWN*   
要扫描其循环的 FL 端口类型端口的全球名称 \_ 。 此信息将传送到 SendSRL 结构中的 **WWN** 成员的微型端口驱动程序 \_ 。

*域名*   
要扫描其循环的域的域号。 此信息将传送到结构中 SendSRL 的 **域** 成员的微型端口驱动程序 \_ 。

*TotalRspBufferSize*   
SRL 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 [**SendSRL \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构的 **TotalRspBufferSize** 成员中返回此信息。

*ActualRspBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 [**SendSRL \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构的 **ActualRspBufferSize** 成员中返回此信息。

*RspBuffer*   
SRL 命令的结果。 微型端口驱动程序在 [**SendSRL \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构的 **RspBuffer** 成员中返回此信息。

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

\_ [ **SendSRL \_ OUT** 中的 SendSRL](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)

 

