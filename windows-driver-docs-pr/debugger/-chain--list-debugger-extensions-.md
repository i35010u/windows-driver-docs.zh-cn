---
title: .chain （列表调试器扩展）
description: .Chain 命令将列出其默认的搜索顺序中的所有已加载的调试器扩展。
ms.assetid: 73139b02-265a-424d-9de8-f4f3736e62db
keywords:
- .chain （列表调试器扩展） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .chain (List Debugger Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd87e6c1863a3ad9e1883c40fefc7f8e137e30a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533202"
---
# <a name="chain-list-debugger-extensions"></a>.chain （列表调试器扩展）


**.Chain**命令将列出其默认的搜索顺序中的所有已加载的调试器扩展。

```dbgsyntax
.chain
.chain /D
```

## <a name="span-idddkmetaclosehandledbgspanspan-idddkmetaclosehandledbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>参数


<span id="________D______"></span><span id="________d______"></span> **/D**   
显示输出使用[调试器标记语言](debugger-markup-language-commands.md)。 在输出中，每个列出的模块是可单击以获取有关模块实现的扩展信息的链接。

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
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关加载的详细信息，卸载，并控制扩展，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。 执行扩展命令和默认的搜索顺序的说明的详细信息，请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)。

 

 





