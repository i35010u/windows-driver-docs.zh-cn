---
title: .scroll_prefs（控制源滚动首选项）
description: 当滚动到一行时，.scroll_prefs 命令控制源在源窗口中的位置。
keywords:
- .scroll_prefs (控制源代码滚动首选项) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scroll_prefs (Control Source Scrolling Preferences)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25ebd62db56aa450147a1479f0fbdd8251e85113
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793313"
---
# <a name="scroll_prefs-control-source-scrolling-preferences"></a>。 scroll \_ prefs (控件源代码滚动首选项) 


当滚动到一行时， **scroll \_ prefs** 命令控制源在源窗口中的位置。

```dbgcmd
.scroll_prefs Before After 
.scroll_prefs 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Before______"></span><span id="_______before______"></span><span id="_______BEFORE______"></span>*之前*   
指定要滚动的行之前的多少源行应在源窗口中可见。

<span id="_______After______"></span><span id="_______after______"></span><span id="_______AFTER______"></span>*后*   
指定滚动行之后的源行数应在源窗口中可见。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，不能在脚本文件中使用。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果将此命令与无参数一起使用，则将显示当前的源代码滚动首选项。

 

 





