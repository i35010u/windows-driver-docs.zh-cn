---
title: gle
description: Gle 扩展显示当前线程的最后一个错误值。
ms.assetid: bed3ce17-6860-421f-ae20-11faa50310ed
keywords:
- 线程，错误值
- 错误值
- gle Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96999935de0da5711fb8a36c647070d015c3a254
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716854"
---
# <a name="gle"></a>!gle


**！ Gle** extension 显示当前线程的最后一个错误值。

```dbgcmd
!gle [-all]
```

## <a name="span-idddk__gle_dbgspanspan-idddk__gle_dbgspanparameters"></a><span id="ddk__gle_dbg"></span><span id="DDK__GLE_DBG"></span>参数


<span id="_______-all______"></span><span id="_______-ALL______"></span>**-所有**   
显示目标系统上每个用户模式线程的最后一个错误。 如果在用户模式下省略此参数，则调试器将显示当前线程的最后一个错误。 如果在内核模式中省略此参数，则调试器将显示当前 [注册上下文](changing-contexts.md#register-context) 指定的线程的最后一个错误。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Ext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 [**GetLastError**](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 例程的详细信息，请参阅 Micorosft Windows SDK 文档。

<a name="remarks"></a>备注
-------

**！ Gle** Extension 显示[**GetLastError**](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)的值，并尝试对此值进行解码。

在内核模式下，仅当调试器可以读取线程环境块 (TEB) 时， **！ gle** 扩展才有效。

 

