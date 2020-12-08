---
title: .chain（列出调试器扩展）
description: 链式命令按默认搜索顺序列出所有已加载的调试器扩展。
keywords:
- " (在) Windows 调试中列出调试器扩展"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .chain (List Debugger Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b71ad72c298c61269a869ef1d682307774e1af1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814077"
---
# <a name="chain-list-debugger-extensions"></a>.chain（列出调试器扩展）


**链式** 命令按默认搜索顺序列出所有已加载的调试器扩展。

```dbgsyntax
.chain
.chain /D
```

## <a name="span-idddk_meta_close_handle_dbgspanspan-idddk_meta_close_handle_dbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>参数


<span id="________D______"></span><span id="________d______"></span>**/D**   
使用 [调试器标记语言](debugger-markup-language-commands.md)显示输出。 在输出中，每个列出的模块都是一个链接，你可以单击该链接来获取有关该模块实现的扩展的信息。

## <span id="ddk_meta_list_debugger_extensions_dbg"></span><span id="DDK_META_LIST_DEBUGGER_EXTENSIONS_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关加载、卸载和控制扩展的详细信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。 有关执行扩展命令和默认搜索顺序说明的详细信息，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md)。

 

 





