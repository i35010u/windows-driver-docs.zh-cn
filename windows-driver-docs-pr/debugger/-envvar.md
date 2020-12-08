---
title: envvar
description: Envvar 扩展显示指定环境变量的值。
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
ms.openlocfilehash: 498b4f6f8f29720ded0b93fdbb90c1548e4b79ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819449"
---
# <a name="envvar"></a>!envvar


**！ Envvar** 扩展显示指定环境变量的值。

```dbgcmd
!envvar Variable
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span>*变量*   
指定显示其值的环境变量。 *变量* 不区分大小写。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关环境变量的详细信息，请参阅 [环境变量](environment-variables.md) 和 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

**！ Envvar** 扩展在用户模式和内核模式下均可正常工作。 但是，在内核模式下，将空闲线程设置为当前进程时，指向进程环境块 (的指针) 为 **NULL**，因此它将失败。 在内核模式下， **！ envvar** 扩展显示目标计算机上的环境变量，如下例所示。

```dbgcmd
0:000> !envvar _nt_symbol_path
        _nt_symbol_path = srv*C:\mysyms*https://msdl.microsoft.com/download/symbols
```

 

 





