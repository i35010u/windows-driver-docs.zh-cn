---
title: .fiximports （修复目标模块导入）
description: .Fiximports 命令验证并更正目标模块的所有静态导入链接。
ms.assetid: 584a5060-5ab5-4126-bfec-e2fe647d50ff
keywords:
- 修复目标模块导入 (.fiximports) 命令
- .fiximports （修复目标模块导入） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiximports (Fix Target Module Imports)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92a5ef997dc3ae8bc85d4bb762a93994e6b38ad1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523341"
---
# <a name="fiximports-fix-target-module-imports"></a>.fiximports （修复目标模块导入）


**.Fiximports**命令验证并更正目标模块的所有静态导入链接。

```dbgcmd
.fiximports Module
```

## <a name="span-idddkmetafixtargetmoduleimportsdbgspanspan-idddkmetafixtargetmoduleimportsdbgspanparameters"></a><span id="ddk_meta_fix_target_module_imports_dbg"></span><span id="DDK_META_FIX_TARGET_MODULE_IMPORTS_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定目标模块调试器更正其导入。 *模块*可以包含各种通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。 如果你想要中包括空格*模块*，必须将参数括在引号中。

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
<td align="left"><p>崩溃转储唯一 （小型转储仅）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用 **.fiximports**命令只有当目标是小型转储不包含其自己的可执行映像。

当调试器将映射为内存使用的映像时，调试器不会自动连接映像导入到导出程序。 因此，请参阅导入的说明被拆装如一个实时调试会话中所示相同的方式。 可以使用 **.fiximports**请求调试器执行相应的导入链接。

 

 





