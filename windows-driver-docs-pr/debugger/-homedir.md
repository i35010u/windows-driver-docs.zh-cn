---
title: 主目录
description: 主目录扩展设置符号服务器和源服务器使用的默认目录。
ms.assetid: 6bebd7df-03d8-4413-8a0c-a0d5ad913173
keywords:
- Windows 调试的主目录
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- homedir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74e85ade59232c03a23146028e52eb060288e296
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555890"
---
# <a name="homedir"></a>！ 主目录


**！ Homedir**扩展设置符号服务器和源服务器使用的默认目录。

```dbgcmd
!homedir Directory
!homedir
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *Directory*   
指定要使用作为主目录的新目录。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

如果 **！ homedir**扩展不带参数，则显示当前的主目录。

对于源服务器缓存位于主目录的子目录中。 符号服务器的下游存储默认到主目录的符号子目录，除非指定了不同的位置。

当启动 WinDbg 时，主目录是已安装的 Windows 调试工具的目录。 **！ Homedir**扩展可用于更改此值。

 

 





