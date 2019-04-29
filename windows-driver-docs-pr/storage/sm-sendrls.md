---
title: SM\_SendRLS 函数
description: SM\_SendRLS WMI 方法通过指定的本地端口发送读取的链接状态 (RLS)。 此 RLS 与所指示的远程端口发送，以检索与远程端口相关联的链接错误状态块。
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
ms.openlocfilehash: 86a2da5a4c0210f281cfaf56968757cab19960db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378927"
---
# <a name="smsendrls-function"></a>SM\_SendRLS 函数


SM\_SendRLS WMI 方法通过指定的本地端口发送读取的链接状态 (RLS)。 此 RLS 与所指示的远程端口发送，以检索与远程端口相关联的链接错误状态块。

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

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
通过其发送的 RLS 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM HbaPortWWN 成员中的微型端口驱动程序\_SendRLS\_结构中。

*DestWWN*   
目标端口全球通用名称 (WWN)。 此信息传递到 SM DestWWN 成员中的微型端口驱动程序\_SendRLS\_结构中。

*InRespBufferMaxSize*   
以字节为单位，响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_SendRLS\_结构。

*TotalRespBufferSize*   
以字节为单位，RLS 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRespBufferSize 成员\_SendRLS\_结构。

*OutRespBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM OutRespBufferSize 成员\_SendRLS\_结构。

*RespBuffer*   
RLS 命令的结果。 微型端口驱动程序返回此信息在 SM RespBuffer 成员\_SendRLS\_结构。

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

[**SM\_SendRLS\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566305)

 

 






