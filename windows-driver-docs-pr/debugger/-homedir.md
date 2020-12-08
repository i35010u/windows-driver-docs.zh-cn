---
title: homedir
description: Homedir 扩展设置符号服务器和源服务器使用的默认目录。
keywords:
- homedir Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- homedir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8750bcf2c02fe34927c86e33c397e7d758f70c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825821"
---
# <a name="homedir"></a>!homedir


**！ Homedir** extension 设置符号服务器和源服务器使用的默认目录。

```dbgcmd
!homedir Directory
!homedir
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span>*目录*   
指定要用作主目录的新目录。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 **！ homedir** 扩展与 no 参数一起使用，则将显示当前主目录。

源服务器的缓存位于主目录的 src 子目录中。 除非指定了其他位置，否则符号服务器的下游存储默认为主目录的符号子目录。

当 WinDbg 启动时，主目录是用于安装 Windows 调试工具的目录。 **！ Homedir** 扩展可用于更改此值。

 

 





