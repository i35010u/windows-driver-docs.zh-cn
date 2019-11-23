---
title: SM\_SendLIRR 函数
description: SM\_SendLIRR WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册（LIRR）命令。
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
ms.openlocfilehash: 0231e283b74e88a692be2d2194bb4def07f77322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845461"
---
# <a name="sm_sendlirr-function"></a>SM\_SendLIRR 函数


SM\_SendLIRR WMI 方法通过指定的本地端口向指定的远程端口发送链接事件记录注册（LIRR）命令。

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
用于发送 LIRR 命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendLIRR 的 SourceWWN 成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendLIRR 的 DestWWN 成员中的微型端口驱动程序。

*函数*   
标识要执行的注册函数的代码。 有关可分配给此成员的值的说明，请参阅 T11 委员会光纤通道组帧和信号规范。 此信息将传送到 SM\_SendLIRR\_在结构中的功能成员的微型端口驱动程序中。

*类型*   
请求其链接信息的设备类型。 有关可分配给此成员的值的说明，请参阅 T11 委员会*光纤通道组帧和信号*规范。 此信息将传送到 SM\_SendLIRR\_在结构中的功能成员的微型端口驱动程序中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小（以字节为单位）。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_SendLIRR\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalRespBufferSize*   
LIRR 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendLIRR\_OUT 结构的 TotalRespBufferSize 成员中返回此信息。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendLIRR\_OUT 结构的 OutRespBufferSize 成员中返回此信息。

*RespBuffer*   
LIRR 命令的结果。 微型端口驱动程序在 SM\_SendLIRR\_OUT 结构的 RespBuffer 成员中返回此信息。

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

[**SM\_SendLIRR\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendlirr_out)

 

 






