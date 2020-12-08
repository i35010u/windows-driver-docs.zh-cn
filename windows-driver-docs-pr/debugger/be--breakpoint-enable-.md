---
title: be（断点启用）
description: "\"是\" 命令还原之前已禁用的一个或多个断点。"
keywords:
- " (断点启用) Windows 调试"
ms.date: 09/18/2019
topic_type:
- apiref
api_name:
- be (Breakpoint Enable)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8082e3469d69e358bc44648d7a2add3bad692da6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838371"
---
# <a name="be-breakpoint-enable"></a>be（断点启用）

" **是** " 命令还原之前已禁用的一个或多个断点。

```dbgcmd
be Breakpoints 
```

## <a name="span-idddk_cmd_breakpoint_enable_dbgspanspan-idddk_cmd_breakpoint_enable_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_enable_dbg"></span><span id="DDK_CMD_BREAKPOINT_ENABLE_DBG"></span>参数

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span>*断点*   
指定要启用的断点的 ID 号。 可以指定任意数量的断点。 必须用空格或逗号分隔多个 Id。 可以通过使用连字符 ( ) 来指定断点 Id 的范围。 可以使用星号 (\*) 来指示所有断点。 如果要对 ID 使用 [数值表达式](numerical-expression-syntax.md) ，请将其括在括号中， (\[ \]) 。 如果要使用 [带有通配符的字符串](string-wildcard-syntax.md) 来匹配断点的符号名称，请将其括在引号中 ( "" ) 。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用断点、其他断点命令和控制断点的方法以及如何在用户空间中从内核调试器设置断点的详细信息，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

使用 [**bl (断点列表)**](bl--breakpoint-list-.md) 命令可列出所有现有断点、其 ID 号及其状态。

使用 [**bpcmds (显示断点命令)**](-bpcmds--display-breakpoint-commands-.md) 命令可列出所有现有断点、其 ID 号以及用于创建它们的命令。
