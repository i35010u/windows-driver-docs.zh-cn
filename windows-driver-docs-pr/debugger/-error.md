---
title: 错误
description: 错误扩展解码，并显示一个错误值有关的信息。
ms.assetid: 4999ab4b-2f55-47d4-b9a7-6f1231271fcc
keywords:
- 错误代码
- Win32 错误代码
- WinSock 错误代码
- Windows 调试错误
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- error
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52979ccbfc69d9f31a38f833e4552d15e3e9a2d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334515"
---
# <a name="error"></a>!error


**！ 错误**扩展进行解码，并显示一个错误值有关的信息。

```dbgcmd
!error Value [Flags]
```

## <a name="span-idddkerrordbgspanspan-idddkerrordbgspanparameters"></a><span id="ddk__error_dbg"></span><span id="DDK__ERROR_DBG"></span>参数


<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定以下的错误代码之一：

-   Win32

-   Winsock

-   NTSTATUS

-   NetAPI

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
如果*标志*设置为 1，错误代码读取为 NTSTATUS 代码。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面的示例演示如何使用 **！ 错误**。

```dbgcmd
0:000> !error 2
Error code: (Win32) 0x2 (2) - The system cannot find the file specified.
0:000> !error 2 1
Error code: (NTSTATUS) 0x2 - STATUS_WAIT_2
```

 

 





