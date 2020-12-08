---
title: .extmatch（显示所有匹配的扩展）
description: Extmatch 命令显示当前加载的扩展 Dll （与指定的模式匹配）导出的扩展命令。
keywords:
- extmatch (显示) Windows 调试的所有匹配扩展
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extmatch (Display All Matching Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30c9518a78156c1a8f5e0d90c74f0393a8bcc454
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819425"
---
# <a name="extmatch-display-all-matching-extensions"></a>.extmatch（显示所有匹配的扩展）


**Extmatch** 命令显示当前加载的扩展 dll （与指定的模式匹配）导出的扩展命令。

```dbgcmd
.extmatch [Options] Pattern 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定搜索选项。 您可以使用以下一个或多个选项：

<span id="_e_ExtDLLPattern"></span><span id="_e_extdllpattern"></span><span id="_E_EXTDLLPATTERN"></span>**/e**  **** *ExtDLLPattern*  
将枚举限制为与指定模式字符串匹配的扩展 Dll 导出的扩展命令。 *ExtDLLPattern* 与扩展 DLL 文件名匹配。

<span id="_n"></span><span id="_N"></span>**/n**  
显示扩展时排除扩展名。 因此，如果指定了此选项，则只会显示扩展名称本身。

<span id="________D______"></span><span id="________d______"></span>**/D**   
使用 [调试器标记语言 (DML) ](debugger-markup-language-commands.md)显示输出。 在输出中，每个列出的扩展都是一个链接，你可以单击该链接来获取有关扩展的详细信息。 并非所有扩展模块都支持 DML。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定扩展必须包含的模式。 *模式* 可以包含各种通配符和说明符。 有关语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

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

若要显示加载的扩展 Dll 的列表，请使用 [**链式**](-chain--list-debugger-extensions-.md) 命令。

下面是此命令的一个示例，其中显示了导出命名为！ help 的所有加载的扩展 Dll：

```dbgcmd
0:000> .extmatch help 
!ext.help
!exts.help
!uext.help
!ntsdexts.help
```

下面的示例列出了以字符串 "he" 开头的所有扩展命令，这些扩展 Dll 的名称以字符串 "ex" 开头：

```dbgcmd
0:000> .extmatch /e ext* he* 
!ext.heap
!ext.help
!exts.heap
!exts.help
```

下面的示例列出了所有扩展命令，因此，我们可以看到哪些扩展命令支持 DML。

![extmatch/d 输出的屏幕截图](images/extmatch01.png)

 

 





