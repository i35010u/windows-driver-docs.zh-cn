---
title: .fiximports（修复目标模块导入）
description: Fiximports 命令验证并更正目标模块的所有静态导入链接。
keywords:
- 修复目标模块导入 ( fiximports) 命令
- fiximports (修复目标模块导入) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiximports (Fix Target Module Imports)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5cd6a9b39e6bce31771a7486aa3403a61770e4fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815535"
---
# <a name="fiximports-fix-target-module-imports"></a>.fiximports（修复目标模块导入）


**Fiximports** 命令验证并更正目标模块的所有静态导入链接。

```dbgcmd
.fiximports Module
```

## <a name="span-idddk_meta_fix_target_module_imports_dbgspanspan-idddk_meta_fix_target_module_imports_dbgspanparameters"></a><span id="ddk_meta_fix_target_module_imports_dbg"></span><span id="DDK_META_FIX_TARGET_MODULE_IMPORTS_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定调试器纠正其导入的目标模块。 *模块* 可以包含各种通配符和说明符。 有关语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。 如果要在 *模块* 中包含空格，则必须用引号将参数引起来。

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
<td align="left"><p>仅限 (仅限小型转储) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅当目标是不包含其自己的可执行映像的小型转储时，才能使用 **fiximports** 命令。

当调试器映射用于作为内存的图像时，调试器不会将图像导入自动连接到导出程序。 因此，以与实时调试会话中相同的方式反汇编引用导入的指令。 可以使用 **. fiximports** 请求调试器执行适当的导入链接。

 

 





