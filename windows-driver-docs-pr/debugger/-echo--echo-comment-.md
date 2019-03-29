---
title: .echo（Echo 注释）
description: .Echo 命令显示注释字符串。
ms.assetid: 4a291952-695c-4292-8aa5-82d497f0141c
keywords:
- .echo （Echo 注释） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echo (Echo Comment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf1befcd5327060bf1e2c924ee4171ac7f3a4e56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566667"
---
# <a name="echo-echo-comment"></a>.echo（Echo 注释）


**.Echo**命令显示注释字符串。

```dbgcmd
.echo String 
.echo "String" 
```

## <a name="span-idddkmetaechocommentdbgspanspan-idddkmetaechocommentdbgspanparameters"></a><span id="ddk_meta_echo_comment_dbg"></span><span id="DDK_META_ECHO_COMMENT_DBG"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
指定要显示的文本。 此外可以包含*字符串*用引号 （"）。 无论使用引号中，*字符串*可以包含任意数量的空格、 逗号和单引号 （'） 引起来。 如果将括*字符串*在引号中，它可以包含分号，但不是额外的引号。 如果您不能将放*字符串*在引号中，它可以包含除第一个字符的任何位置中的引号，但它不能包含分号。

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

**.Echo**命令将导致调试器以显示*字符串*立即输入命令后。

**.Echo**命令结束如果调试器遇到分号 （除非分号出现在带引号的字符串）。 此限制，您可以使用 **.echo**在复杂的构造，如[条件断点](setting-a-conditional-breakpoint.md)，如下面的示例所示。

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
```

**.Echo**命令还提供了一种简便方法，调试服务器和调试客户端进行相互通信的用户。 有关这种情况的详细信息，请参阅[控制远程调试会话](controlling-a-remote-debugging-session.md)。

**.Echo**命令有所不同[ **$$ （注释说明符）** ](-----comment-specifier-.md)令牌并[  **\* （注释行说明符）**](----comment-line-specifier-.md)令牌，因为这些令牌会导致调试器忽略输入的文本而不会显示它。

 

 





