---
title: ln （列出最近的符号）
description: Ln 命令显示的符号处或附近的给定的地址。
ms.assetid: ff01ace7-398a-4e32-9d58-00873eca3201
keywords:
- ln （列出最近的符号） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ln (List Nearest Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ded9b73fb0ab3adcddd7f754eb367fe2f8dc0ec2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519669"
---
# <a name="ln-list-nearest-symbols"></a>ln （列出最近的符号）


**Ln**命令显示的符号处或附近的给定的地址。

```dbgcmd
ln Address
ln /D Address 
```

## <a name="span-idddkcmdlistnearestsymbolsdbgspanspan-idddkcmdlistnearestsymbolsdbgspanparameters"></a><span id="ddk_cmd_list_nearest_symbols_dbg"></span><span id="DDK_CMD_LIST_NEAREST_SYMBOLS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定调试器应开始搜索符号的位置的地址。 最接近的符号之前, 或之后*地址*，会显示。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_D"></span><span id="_d"></span>**/D**  
指定使用显示的输出[调试器标记语言 (DML)](debugger-markup-language-commands.md)。 DML 输出包含可用于浏览包含最近的符号的模块的链接。 它还包括可用于设置断点的链接。

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

 

<a name="remarks"></a>备注
-------

可以使用**ln**以帮助确定指针所指向的命令。 当您查看时损坏的堆栈来确定哪个过程进行调用时，此命令也可以是很有用。

如果源代码行信息可用， **ln**显示内容还包括源文件名称和行号信息。

如果使用的[源服务器](using-a-source-server.md)，则**ln**命令将显示与源服务器相关的信息。

 

 





