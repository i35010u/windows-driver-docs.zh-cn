---
title: .symfix（设置符号存储路径）
description: .Symfix 命令自动设置符号路径以指向 Microsoft 符号存储区。
ms.assetid: 9ad80217-e2d1-4776-a620-f2735b2c8f84
keywords:
- 设置符号存储区路径 (.symfix) 命令
- SymSrv，设置符号存储区路径 (.symfix) 命令
- .symfix （设置符号存储区路径） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symfix (Set Symbol Store Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 422fa5e208c6d4714f74cdd6470b993404965e78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562495"
---
# <a name="symfix-set-symbol-store-path"></a>.symfix（设置符号存储路径）


**.Symfix**命令会自动设置符号路径以指向 Microsoft 符号存储区。

```dbgcmd
.symfix[+] [LocalSymbolCache]
```

## <a name="span-idddkmetasetsymbolstorepathdbgspanspan-idddkmetasetsymbolstorepathdbgspanparameters"></a><span id="ddk_meta_set_symbol_store_path_dbg"></span><span id="DDK_META_SET_SYMBOL_STORE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
会导致 Microsoft 符号存储区路径追加到现有的符号路径。 如果这不包括，则替换现有的符号路径。

<span id="_______LocalSymbolCache______"></span><span id="_______localsymbolcache______"></span><span id="_______LOCALSYMBOLCACHE______"></span> *LocalSymbolCache*   
指定要用作本地符号缓存目录。 如果此目录不存在，则它将创建符号服务器开始复制文件时。 如果*LocalSymbolCache*是省略，就将使用调试器安装目录的符号子目录。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[使用符号服务器和符号存储区](symbol-stores-and-symbol-servers.md)。

<a name="remarks"></a>备注
-------

下面的示例演示如何使用 **.symfix**设置新的符号路径指向 Microsoft 符号存储区。

```dbgcmd
3: kd> .symfix c:\myCache
3: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

下面的示例演示如何使用 **.symfix +** 追加指向 Microsoft 符号存储区的路径与现有的符号路径。

```dbgcmd
3: kd> .sympath
Symbol search path is: c:\someSymbols
Expanded Symbol search path is: c:\somesymbols
3: kd> .symfix+ c:\myCache
3: kd> .sympath
Symbol search path is: c:\someSymbols;srv*
Expanded Symbol search path is: c:\somesymbols;cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

 

 





