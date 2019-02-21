---
title: .copysym （复制符号文件）
description: .Copysym 命令将当前的符号文件复制到指定的目录。
ms.assetid: f90d1402-4bf3-4cd0-993e-a42c220beb7a
keywords:
- .copysym （复制符号文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .copysym (Copy Symbol Files)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4882da268e2f74ad4d9f832241bb14a1142814c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519971"
---
# <a name="copysym-copy-symbol-files"></a>.copysym （复制符号文件）


**.Copysym**命令将当前的符号文件复制到指定的目录。

```dbgsyntax
    .copysym [/l] Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________l______"></span><span id="________L______"></span> **/l**   
导致要加载，因为它复制每个符号文件。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
指定符号文件应复制到的目录。 副本不会覆盖现有文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

很多时候，符号存储在网络中。 符号访问通常会很慢，或者可能需要传输到另一台计算机，你不再具有网络访问权限在调试会话。 在这种情况下， **.copysym**命令可用于复制所需的会话与本地目录的符号。

 

 





