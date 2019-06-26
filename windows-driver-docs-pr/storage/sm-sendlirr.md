---
title: SM\_SendLIRR 函数
description: SM\_SendLIRR WMI 方法将通过指示本地端口链接事件记录注册 (LIRR) 命令发送到所指示的远程端口。
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
ms.openlocfilehash: 05c6a4fcfb6c3da06e2c136e4e63c470ae96ebf3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384288"
---
# <a name="smsendlirr-function"></a>SM\_SendLIRR 函数


SM\_SendLIRR WMI 方法将通过指示本地端口链接事件记录注册 (LIRR) 命令发送到所指示的远程端口。

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

<a name="parameters"></a>Parameters
----------

*SourceWWN*   
通过其发送 LIRR 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM SourceWWN 成员中的微型端口驱动程序\_SendLIRR\_结构中。

*DestWWN*   
目标端口全球通用名称 (WWN)。 此信息传递到 SM DestWWN 成员中的微型端口驱动程序\_SendLIRR\_结构中。

*函数*   
标识哪个注册函数的代码是执行。 有关这些值可以分配给此成员说明，请参阅 T11 委员会的光纤通道组帧和信号发送规范。 此信息传递到 SM 的函数成员中的微型端口驱动程序\_SendLIRR\_结构中。

*类型*   
哪些链接请求信息的设备类型。 这些值可以分配给此成员说明，请参阅 T11 委员会*光纤通道组帧和信号发送*规范。 此信息传递到 SM 的函数成员中的微型端口驱动程序\_SendLIRR\_结构中。

*InRespBufferMaxSize*   
以字节为单位，响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_SendLIRR\_结构。

*TotalRespBufferSize*   
以字节为单位，LIRR 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRespBufferSize 成员\_SendLIRR\_结构。

*OutRespBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM OutRespBufferSize 成员\_SendLIRR\_结构。

*RespBuffer*   
LIRR 命令的结果。 微型端口驱动程序返回此信息在 SM RespBuffer 成员\_SendLIRR\_结构。

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

[**SM\_SendLIRR\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_sendlirr_out)

 

 






