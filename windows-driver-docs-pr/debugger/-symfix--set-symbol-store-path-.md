---
title: .symfix（设置符号存储路径）
description: Symfix 命令自动将符号路径设置为指向 Microsoft 符号存储区。
keywords:
- 设置符号存储区路径 ( symfix) 命令
- SymSrv，设置符号存储区路径 (. symfix) 命令
- symfix (设置符号存储区路径) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symfix (Set Symbol Store Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22e5eb56a91b7f62ec0e29d8429777d2e9d33902
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832029"
---
# <a name="symfix-set-symbol-store-path"></a>.symfix（设置符号存储路径）


**Symfix** 命令自动将符号路径设置为指向 Microsoft 符号存储区。

```dbgcmd
.symfix[+] [LocalSymbolCache]
```

## <a name="span-idddk_meta_set_symbol_store_path_dbgspanspan-idddk_meta_set_symbol_store_path_dbgspanparameters"></a><span id="ddk_meta_set_symbol_store_path_dbg"></span><span id="DDK_META_SET_SYMBOL_STORE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
使 Microsoft 符号存储区路径追加到现有符号路径上。 如果未包括此方法，则将替换现有的符号路径。

<span id="_______LocalSymbolCache______"></span><span id="_______localsymbolcache______"></span><span id="_______LOCALSYMBOLCACHE______"></span>*LocalSymbolCache*   
指定要用作本地符号缓存的目录。 如果此目录不存在，则会在符号服务器开始复制文件时创建。 如果省略 *LocalSymbolCache* ，则将使用调试器安装目录的符号子目录。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [使用符号服务器和符号存储](symbol-stores-and-symbol-servers.md)。

<a name="remarks"></a>备注
-------

下面的示例演示如何使用 **symfix** 来设置指向 Microsoft 符号存储区的新符号路径。

```dbgcmd
3: kd> .symfix c:\myCache
3: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

下面的示例演示如何使用 **. symfix +** 将现有符号路径追加到指向 Microsoft 符号存储区的路径。

```dbgcmd
3: kd> .sympath
Symbol search path is: c:\someSymbols
Expanded Symbol search path is: c:\somesymbols
3: kd> .symfix+ c:\myCache
3: kd> .sympath
Symbol search path is: c:\someSymbols;srv*
Expanded Symbol search path is: c:\somesymbols;cache*c:\myCache;SRV*https://msdl.microsoft.com/download/symbols
```

 

 





