---
title: SendRLS 函数
description: SendRLS WMI 方法将通过指示本地端口读取的链接错误状态块 (RLS) 发送到指定的远程端口来检索与远程端口相关联的链接错误状态块。
ms.assetid: 57dcc810-023f-4dbf-a9c2-3062765729c7
keywords:
- SendRLS 函数存储设备
topic_type:
- apiref
api_name:
- SendRLS
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02121f426a757a068598e603dbf99101acaeb99d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519074"
---
# <a name="sendrls-function"></a>SendRLS 函数


**SendRLS** WMI 方法将通过指示本地端口读取的链接错误状态块 (RLS) 发送到所指示的远程端口来检索与远程端口相关联的链接错误状态块。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRLS(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendRLS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565452)结构。

*PortWWN*   
通过其发送的 RLS 命令的本地端口全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **SendRLS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565446)结构。

*DestWWN*   
目标端口全球通用名称。 此信息传递到中的微型端口驱动程序**DestWWN**的成员[ **SendRLS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565446)结构。

*TotalRspBufferSize*   
以字节为单位的 RLS 命令的结果大小。 微型端口驱动程序将返回此信息**TotalRspBufferSize**的成员[ **SendRLS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565452)结构。

*ActualRspBufferSize*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualRspBufferSize**的成员[ **SendRLS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565452)结构。

*RspBuffer*   
RLS 命令的结果。 微型端口驱动程序将返回此信息**RspBuffer**的成员[ **SendRLS\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565452)结构。

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
<td align="left"><p>标头</p></td>
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

[**SendRLS\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565446)

[**SendRLS\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565452)

 

 






