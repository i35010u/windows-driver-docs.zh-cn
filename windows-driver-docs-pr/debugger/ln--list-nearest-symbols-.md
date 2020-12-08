---
title: ln（列出最接近的符号）
description: Ln 命令显示给定地址附近或附近的符号。
keywords:
- ln (列出最接近的符号) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ln (List Nearest Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18c23e43af8e602605c4018df06a6392242dea7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838171"
---
# <a name="ln-list-nearest-symbols"></a>ln（列出最接近的符号）


**Ln** 命令显示给定地址附近或附近的符号。

```dbgcmd
ln Address
ln /D Address 
```

## <a name="span-idddk_cmd_list_nearest_symbols_dbgspanspan-idddk_cmd_list_nearest_symbols_dbgspanparameters"></a><span id="ddk_cmd_list_nearest_symbols_dbg"></span><span id="DDK_CMD_LIST_NEAREST_SYMBOLS_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定调试器在搜索符号时应开始执行的地址。 将显示最近的符号（在 *Address* 之前或之后）。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_D"></span><span id="_d"></span>**/D**  
指定使用 [调试器标记语言 (DML) ](debugger-markup-language-commands.md)显示输出。 DML 输出包含一个链接，您可以使用该链接浏览包含最近符号的模块。 它还包括一个可用于设置断点的链接。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用 **ln** 命令来帮助确定指针所指向的内容。 当你查看损坏的堆栈以确定调用了哪个过程时，此命令也会很有用。

如果源行信息可用，则 **ln** 显示还包含源文件名和行号信息。

如果正在使用 [源服务器](using-a-source-server.md)，则 **ln** 命令显示与源服务器相关的信息。

 

 





