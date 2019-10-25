---
title: SM\_SendSRL 函数
description: SM\_SendSRL WMI 方法通过所指示的端口向所指示的域控制器发送扫描远程循环（SRL）命令。
ms.assetid: 44090e8d-ffb2-48a9-a574-5bf067ffa952
keywords:
- SM_SendSRL 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendSRL
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 48aa5f53278063beccf884512293d3352a8117bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845452"
---
# <a name="sm_sendsrl-function"></a>SM\_SendSRL 函数


SM\_SendSRL WMI 方法通过所指示的端口向所指示的域控制器发送扫描远程循环（SRL）命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendSRL(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              WWN[8],
   [in] uint32                                 Domain,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
用于发送 SRL 命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendSRL 的 HbaPortWWN 成员中的微型端口驱动程序。

*WWN*   
类型为 FL\_端口的全球通用名称（WWN），将扫描其循环。 此信息将传送到 SM\_SendSRL\_在结构中 WWN 成员的微型端口驱动程序中。

*域*   
要扫描其循环的域的域号。 此信息将传送到 SM\_SendSRL\_的域成员中的微型端口驱动程序。

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

[**SM\_SendSRL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendsrl_out)

 

 






