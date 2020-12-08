---
title: .copysym（复制符号文件）
description: Copysym 命令将当前符号文件复制到指定的目录。
keywords:
- copysym () Windows 调试复制符号文件
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .copysym (Copy Symbol Files)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d94ce58ebc746e2da9e13a925190c955ee8eb8ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803341"
---
# <a name="copysym-copy-symbol-files"></a>.copysym（复制符号文件）


**Copysym** 命令将当前符号文件复制到指定的目录。

```dbgsyntax
    .copysym [/l] Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________l______"></span><span id="________L______"></span>**/l**   
使每个符号文件在被复制时加载。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
指定应将符号文件复制到的目录。 副本不会覆盖现有文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

许多时候，符号存储在网络上。 符号访问通常很慢，或者可能需要将调试会话传输到不再具有网络访问权限的另一台计算机。 在这种情况下，可以使用 **copysym** 命令将会话所需的符号复制到本地目录。

 

 





