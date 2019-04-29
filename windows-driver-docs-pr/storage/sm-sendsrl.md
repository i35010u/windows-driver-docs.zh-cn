---
title: SM\_SendSRL 函数
description: SM\_SendSRL WMI 方法将通过指示端口扫描远程循环 (SRL) 命令发送到指定的域控制器。
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
ms.openlocfilehash: 46a35a2bfec9c970c5c8f44454f0925c3e2362ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380827"
---
# <a name="smsendsrl-function"></a>SM\_SendSRL 函数


SM\_SendSRL WMI 方法将通过指示端口扫描远程循环 (SRL) 命令发送到指定的域控制器。

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

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
通过其发送的 SRL 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM HbaPortWWN 成员中的微型端口驱动程序\_SendSRL\_结构中。

*WWN*   
类型佛罗里达州的端口的全球名称 (WWN)\_其循环是要扫描的端口。 此信息传递到 SM 的 WWN 成员中的微型端口驱动程序\_SendSRL\_结构中。

*域*   
其循环是要扫描的域域数。 此信息传递到 SM 的域成员中的微型端口驱动程序\_SendSRL\_结构中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 SendRPL 在 HBAStatus 成员中返回此信息\_结构。

*TotalRespBufferSize*   
以字节为单位，RPS 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRespBufferSize 成员\_SendRPS\_结构。

*OutRespBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM OutRespBufferSize 成员\_SendRPL\_结构。

*RespBuffer*   
RPS 命令的结果。 微型端口驱动程序返回此信息在 SM RespBuffer 成员\_SendRPS\_结构。

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

[**SM\_SendSRL\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566326)

 

 






