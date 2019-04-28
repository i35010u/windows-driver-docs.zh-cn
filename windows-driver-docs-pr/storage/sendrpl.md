---
title: SendRPL 函数
description: SendRPL WMI 方法将通过指示端口读取的端口列表 (RPL) 命令发送到指定的目标端口。
ms.assetid: 3cf3dfe2-6ff9-431f-b6bf-66ef8dd77df3
keywords:
- SendRPL 函数存储设备
topic_type:
- apiref
api_name:
- SendRPL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0dc71f1aef614860f95fa884aa93e21d7929eb30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343173"
---
# <a name="sendrpl-function"></a>SendRPL 函数


**SendRPL** WMI 方法将通过指示端口读取的端口列表 (RPL) 命令发送到指定的目标端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRPL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                AgentWWN[8],
   [in] uint32                                   agent_domain,
   [in] uint32                                   portIndex,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendRPL\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565503)结构。

*PortWWN*   
通过该发送端口读取的列表 (RPL) 命令的本地端口全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)结构。

*AgentWWN*   
若要查询的 FC 类型的端口列表的端口的全球名称\_端口。 有关定义 FC\_端口，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到中的微型端口驱动程序**AgentWWN**的成员[ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)结构。

*agent\_domain*   
若要查询的 FC 类型的端口列表的域控制器的域号\_端口。 有关定义 FC\_端口，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到中的微型端口驱动程序**代理\_域**的成员[ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)结构。

*portIndex*   
在光纤通道类型的端口列表中的第一个端口的端口索引\_要返回的端口。 此信息传递到中的微型端口驱动程序**portIndex**的成员[ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)结构。

*TotalRspBufferSize*   
以字节为单位的读取的端口列表 (RPL) 命令的结果大小。 微型端口驱动程序将返回此信息**TotalRspBufferSize**的成员[ **SendRPL\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565503)结构。

*ActualRspBufferSize*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualRspBufferSize**的成员[ **SendRPL\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565503)结构。

*RspBuffer*   
读取的结果的端口列表 (RPL) 命令。 微型端口驱动程序将返回此信息**RspBuffer**的成员[ **SendRPL\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565503)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SendRPL\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565496)

[**SendRPL\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565503)

 

 






