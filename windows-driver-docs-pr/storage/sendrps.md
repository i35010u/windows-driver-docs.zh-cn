---
title: SendRPS 函数
description: SendRPS WMI 方法将读取的端口状态块 (RPS) 请求发送到指定的端口或域控制器。
ms.assetid: e8179a42-4095-4c59-81c5-7db7a2985939
keywords:
- SendRPS 函数存储设备
topic_type:
- apiref
api_name:
- SendRPS
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c52a673094b3821c1e80fe6b3b4f60cf44203916
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329984"
---
# <a name="sendrps-function"></a>SendRPS 函数


**SendRPS** WMI 方法将读取的端口状态块 (RPS) 请求发送到指定的端口或域控制器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRPS(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                AgentWWN[8],
   [in, HBAType("HBA_WWN")] uint8                ObjectWWN[8],
   [in] uint32                                   AgentDomain,
   [in] uint32                                   ObjectPortNumber,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendRPS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565516)结构。

*PortWWN*   
通过其发送的 RPS 命令的本地端口全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)结构。

*AgentWWN*   
若要查询的该端口的状态的端口的全球名称指示*ObjectWWN*。 此信息传递到中的微型端口驱动程序**AgentWWN**的成员[ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)结构。

*ObjectWWN*   
全球范围内的端口是要返回状态的端口的名称。 此信息传递到中的微型端口驱动程序**ObjectWWN**的成员[ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)结构。

*AgentDomain*   
所指示该端口的状态要查询的域控制器的域数*ObjectWWN*。 此信息传递到中的微型端口驱动程序**AgentDomain**的成员[ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)结构。

*ObjectPortNumber*   
全球范围内的端口是要返回状态的端口的名称。 此信息传递到中的微型端口驱动程序**ObjectPortNumber**的成员[ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)结构。

*TotalRspBufferSize*   
以字节为单位的 RPS 命令的结果大小。 微型端口驱动程序将返回此信息**TotalRspBufferSize**的成员[ **SendRPS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565516)结构。

*ActualRspBufferSize*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualRspBufferSize**的成员[ **SendRPS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565516)结构。

*RspBuffer*   
RPS 命令的结果。 微型端口驱动程序将返回此信息**RspBuffer**的成员[ **SendRPS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565516)结构。

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

[**SendRPS\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565512)

[**SendRPS\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565516)

 

 






