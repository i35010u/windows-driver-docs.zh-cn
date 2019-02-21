---
title: SM\_SendRPL 函数
description: SM\_SendRPL WMI 方法将通过指示端口读取的端口列表 (RPL) 命令发送到指定的目标端口。
ms.assetid: 9297d5eb-f8c4-48f3-8536-a94c66917e66
keywords:
- SM_SendRPL 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendRPL
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a19413d55e92d1316ad0a72e12a60cbd5f8809b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526924"
---
# <a name="smsendrpl-function"></a>SM\_SendRPL 函数


SM\_SendRPL WMI 方法将通过指示端口读取的端口列表 (RPL) 命令发送到指定的目标端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendRPL(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              AgentWWN[8],
   [in] uint32                                 AgentDomain,
   [in] uint32                                 PortIndex,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
通过该发送端口读取的列表 (RPL) 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM 端口全球通用名称成员中的微型端口驱动程序\_SendRPL\_结构中。

*AgentWWN*   
若要查询的 FC 类型的端口列表的端口的全球名称 (WWN)\_端口。 有关定义 FC\_端口，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到 SM AgentWWN 成员中的微型端口驱动程序\_SendRPL\_结构中。

*AgentDomain*   
若要查询的 FC 类型的端口列表的域控制器的域号\_端口。 有关定义 FC\_端口，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到代理中的微型端口驱动程序\_域成员的 SM\_SendRPL\_结构中。

*PortIndex*   
在光纤通道类型的端口列表中的第一个端口的端口索引\_要返回的端口。 此信息传递到 SM portIndex 成员中的微型端口驱动程序\_SendRPL\_结构中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 SendRPL 在 HBAStatus 成员中返回此信息\_结构。

*TotalRespBufferSize*   
以字节为单位，读取的端口列表 (RPL) 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRespBufferSize 成员\_SendRPL\_结构。

*OutRespBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM OutRespBufferSize 成员\_SendRPL\_结构。

*RespBuffer*   
读取的结果的端口列表 (RPL) 命令。 微型端口驱动程序 SendRPL 在 RespBuffer 成员中返回此信息\_结构。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SendRPL\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566314)

[**SM\_SendRPL\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566315)

 

 






