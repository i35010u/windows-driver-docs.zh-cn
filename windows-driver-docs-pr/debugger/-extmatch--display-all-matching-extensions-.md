---
title: .extmatch（显示所有匹配的扩展）
description: .Extmatch 命令显示当前加载的扩展插件与指定的模式匹配的 Dll 导出的扩展命令。
ms.assetid: 068a32ce-c5ac-4fee-9e9d-e47393097675
keywords:
- .extmatch （显示所有匹配的扩展） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extmatch (Display All Matching Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34b0e8fe39749ce5a29d1ff0cd3f1417296f3b44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337200"
---
# <a name="extmatch-display-all-matching-extensions"></a>.extmatch（显示所有匹配的扩展）


**.Extmatch**命令显示当前加载的扩展插件与指定的模式匹配的 Dll 导出的扩展命令。

```dbgcmd
.extmatch [Options] Pattern 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定的搜索选项。 可以使用一个或多个以下选项：

<span id="_e_ExtDLLPattern"></span><span id="_e_extdllpattern"></span><span id="_E_EXTDLLPATTERN"></span>**/e** **** *ExtDLLPattern*  
限制到扩展命令导出的扩展 Dll 与指定的模式字符串匹配的枚举。 *ExtDLLPattern*与扩展 DLL 文件名匹配。

<span id="_n"></span><span id="_N"></span>**/n**  
显示扩展时，不包括的扩展名称。 因此，如果指定此选项，然后仅本身的扩展名称将显示。

<span id="________D______"></span><span id="________d______"></span> **/D**   
显示输出使用[调试器标记语言 (DML)](debugger-markup-language-commands.md)。 在输出中，每个列出的扩展插件是可单击以获取有关扩展的详细信息的链接。 并非所有扩展模块都支持 DML。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定扩展必须包含的模式。 *模式*可以包含各种通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

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

若要显示已加载的扩展 Dll 的列表，请使用[ **.chain** ](-chain--list-debugger-extensions-.md)命令。

下面是此命令显示所有已加载的扩展具有名为导出的 Dll 的示例 ！ 帮助：

```dbgcmd
0:000> .extmatch help 
!ext.help
!exts.help
!uext.help
!ntsdexts.help
```

以下示例列出了字符串开头的所有扩展命令导出的扩展 Dll 名称以字符串"ex"开头的"he":

```dbgcmd
0:000> .extmatch /e ext* he* 
!ext.heap
!ext.help
!exts.heap
!exts.help
```

下面的示例列出了所有扩展命令，以便我们可以看到哪些支持 DML。

![.extmatch /d 输出的屏幕截图](images/extmatch01.png)

 

 





