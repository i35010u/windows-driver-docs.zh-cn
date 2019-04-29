---
title: SendCTPassThru 函数
description: SendCTPassThru WMI 方法将常见的传输 (CT) 传递命令发送到指定的端口。
ms.assetid: 7f512980-5aff-4359-b52e-7fcef9627e1f
keywords:
- SendCTPassThru 函数存储设备
topic_type:
- apiref
api_name:
- SendCTPassThru
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f1d2e83cfd027776e940032543daddec2bba636
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378530"
---
# <a name="sendctpassthru-function"></a>SendCTPassThru 函数


**SendCTPassThru** WMI 方法将常见的传输 (CT) 传递命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendCTPassThru(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                      PortWWN[8],
   [in] uint32                                         RequestBufferCount,
   [in, WmiSizeIs("RequestBufferCount")] uint8         RequestBuffer[],
   [out] uint32                                        TotalResponseBufferCount,
   [out] uint32                                        ActualResponseBufferCount,
   [out, WmiSizeIs("ActualResponseBufferCount")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendCTPassThru\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565413)结构。

*PortWWN*   
通过它访问目标 HBA 全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)结构。

*RequestBufferCount*   
以字节为单位的缓冲区将保留常见传输命令的结果大小。 微型端口驱动程序将返回此信息**RequestBufferCount**的成员[ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)结构。

*RequestBuffer*   
常见的传输命令的结果。 微型端口驱动程序将返回此信息**RequestBuffer**的成员[ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)结构。

*TotalResponseBufferCount*   
大小 （字节） 的结果常见传输命令。 微型端口驱动程序将返回此信息**TotalResponseBufferCount**的成员[ **SendCTPassThru\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565413)结构。

*ActualResponseBufferCount*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualResponseBufferCount**的成员[ **SendCTPassThru\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565413)结构。

*ResponseBuffer*   
常见的传输命令的结果。 微型端口驱动程序将返回此信息**ResponseBuffer**的成员[ **SendCTPassThru\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565413)结构。

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

[**SendCTPassThru\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565412)

[**SendCTPassThru\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565413)

 

 






