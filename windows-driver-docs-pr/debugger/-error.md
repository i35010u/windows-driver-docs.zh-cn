---
title: error
description: 错误扩展会对错误值进行解码并显示有关的信息。
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
ms.openlocfilehash: 5cca89e177299389144a3a557a10a276dde08828
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820421"
---
# <a name="error"></a>!error


**！错误** 扩展将解码并显示有关错误值的信息。

```dbgcmd
!error Value [Flags]
```

## <a name="span-idddk__error_dbgspanspan-idddk__error_dbgspanparameters"></a><span id="ddk__error_dbg"></span><span id="DDK__ERROR_DBG"></span>参数


<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定以下错误代码之一：

-   Win32

-   Winsock

-   NTSTATUS

-   NetAPI

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
如果 *Flags* 设置为1，则错误代码将作为 NTSTATUS 代码读取。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

下面的示例演示如何使用 **！错误**。

```dbgcmd
0:000> !error 2
Error code: (Win32) 0x2 (2) - The system cannot find the file specified.
0:000> !error 2 1
Error code: (NTSTATUS) 0x2 - STATUS_WAIT_2
```

 

 





