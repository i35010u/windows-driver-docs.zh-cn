---
title: envvar
description: Envvar 扩展显示指定的环境变量的值。
ms.assetid: 7a6e1796-08e0-414e-a092-326b30c8ce8f
keywords:
- envvar Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- envvar
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8da5dffa05b644b6fdeccfa81a4e9fa6ab5f7fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334516"
---
# <a name="envvar"></a>!envvar


**！ Envvar**扩展显示指定的环境变量的值。

```dbgcmd
!envvar Variable
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span> *变量*   
指定其值显示的环境变量。 *变量*不区分大小写。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关环境变量的详细信息，请参阅[环境变量](environment-variables.md)和 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

**！ Envvar**扩展在用户模式下和在内核模式下的作用。 但是，在内核模式下，当为当前进程，设置的空闲线程指针到进程环境块 (PEB) 是**NULL**，因此它将失败。 在内核模式下 **！ envvar**扩展显示的目标计算机上，如以下示例所示的环境变量。

```dbgcmd
0:000> !envvar _nt_symbol_path
        _nt_symbol_path = srv*C:\mysyms*https://msdl.microsoft.com/download/symbols
```

 

 





