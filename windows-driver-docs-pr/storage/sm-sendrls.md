---
title: SM\_SendRLS 函数
description: SM\_SendRLS WMI 方法通过指定的本地端口发送读取链接状态（RLS）。 此 RLS 将发送到指定的远程端口，以检索与远程端口关联的链接错误状态块。
ms.assetid: 4498edde-1249-43b8-b581-37e24f8bd2d3
keywords:
- SM_SendRLS 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendRLS
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d779aeb2d2c17ae6f44ff87a891925c2e2c6123
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845460"
---
# <a name="sm_sendrls-function"></a>SM\_SendRLS 函数


SM\_SendRLS WMI 方法通过指定的本地端口发送读取链接状态（RLS）。 此 RLS 将发送到指定的远程端口，以检索与远程端口关联的链接错误状态块。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendRLS(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              DestWWN[8],
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
用于发送 RLS 命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRLS 的 HbaPortWWN 成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRLS 的 DestWWN 成员中的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小（以字节为单位）。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_SendRLS\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalRespBufferSize*   
RLS 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRLS\_OUT 结构的 TotalRespBufferSize 成员中返回此信息。

*OutRespBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRLS\_OUT 结构的 OutRespBufferSize 成员中返回此信息。

*RespBuffer*   
RLS 命令的结果。 微型端口驱动程序在 SM\_SendRLS\_OUT 结构的 RespBuffer 成员中返回此信息。

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

[**SM\_SendRLS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrls_out)

 

 






