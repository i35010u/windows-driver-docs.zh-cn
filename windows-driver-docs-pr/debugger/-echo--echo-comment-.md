---
title: .echo（Echo 注释）
description: Echo 命令显示注释字符串。
keywords:
- 。回显 (回显注释) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echo (Echo Comment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90eb9ae9eed192cf0b8899583fcc283f7e6c7115
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799875"
---
# <a name="echo-echo-comment"></a>.echo（Echo 注释）


**Echo** 命令显示注释字符串。

```dbgcmd
.echo String 
.echo "String" 
```

## <a name="span-idddk_meta_echo_comment_dbgspanspan-idddk_meta_echo_comment_dbgspanparameters"></a><span id="ddk_meta_echo_comment_dbg"></span><span id="DDK_META_ECHO_COMMENT_DBG"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
指定要显示的文本。 还可以将 *字符串* 括在引号中 ( ") 。 无论是否使用引号， *String* 都可以包含任意数量的空格、逗号和单引号 ( ") 。 如果用引号将 *字符串* 引起来，则可以包含分号，但不能包含其他引号。 如果不将 *字符串* 括在引号中，则它可以在除第一个字符之外的任何位置添加引号，但不能包含分号。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

输入命令后， **echo** 命令会使调试器立即显示 *字符串* 。

如果调试器遇到分号 (将结束 **echo** 命令，除非分号出现在带引号的字符串) 内。 此限制使你能够在复杂构造（如 [条件断点](setting-a-conditional-breakpoint.md)）中使用 **echo** ，如下面的示例所示。

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
```

**Echo** 命令还为调试服务器和调试客户端的用户提供了一种简单的方法来相互通信。 有关此情况的详细信息，请参阅 [控制远程调试会话](controlling-a-remote-debugging-session.md)。

**Echo** 命令不同于 [**$ $ (注释说明符)**](-----comment-specifier-.md)标记和 [**\* (注释行说明符)**](----comment-line-specifier-.md)标记，因为这些标记会使调试器忽略输入文本而不显示它。

 

 





