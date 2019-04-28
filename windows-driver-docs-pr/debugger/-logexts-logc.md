---
title: logexts.logc
description: Logexts.logc 扩展显示 API 的所有类别，都显示特定类别中的所有 Api 或启用和禁用的 Api 中一个或多个类别的日志记录。
ms.assetid: b0132055-da13-45a8-8e83-06ddcb8b90d7
keywords:
- logexts.logc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e773d11624b197bf26fb1bb0ca0811e82d90924c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336127"
---
# <a name="logextslogc"></a>!logexts.logc


**！ Logexts.logc**扩展显示 API 的所有类别，都显示特定类别中的所有 Api 或启用和禁用的 Api 中一个或多个类别的日志记录。

```dbgcmd
!logexts.logc e Categories 
!logexts.logc d Categories 
!logexts.logc p Category 
!logexts.logc 
```

## <a name="span-idddklogextslogcdbgspanspan-idddklogextslogcdbgspanparameters"></a><span id="ddk__logexts_logc_dbg"></span><span id="DDK__LOGEXTS_LOGC_DBG"></span>参数


<span id="_______e______"></span><span id="_______E______"></span> **e**   
启用日志记录功能的指定类别。

<span id="_______d______"></span><span id="_______D______"></span> **d**   
指定类别禁用日志记录功能。

<span id="_______Categories______"></span><span id="_______categories______"></span><span id="_______CATEGORIES______"></span> *类别*   
指定要启用或禁用的类别。 如果列出多个类别，请用空格分隔它们。 一个星号 (\*) 能用来表示所有类别。

<span id="_______p______"></span><span id="_______P______"></span> **p**   
显示属于指定类别的所有 Api。

<span id="_______Category______"></span><span id="_______category______"></span><span id="_______CATEGORY______"></span> *Category*   
指定将显示其 Api 的类别。 可以使用指定只有一个类别**p**选项。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[记录器和日志查看器](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

不带任何选项 **！ logexts.logc**将显示可用类别的当前列表，并将指示启用和禁用哪些功能。

如果禁用了某个类别，因此不再对性能产生影响，将删除该类别中的所有 Api 的挂钩。 COM 挂钩不会删除，因为它们不能在重新启用。

当您只是想特定类型的程序具有与 Windows （例如，文件操作） 的交互时，允许仅某些类别可能会很有用。 这可以减少日志文件大小，而且还可以减少的记录器进程的执行速度上产生的影响。

以下命令将启用所有类别的日志记录：

```dbgcmd
0:000> !logexts.logc e *
```

以下命令将禁用类别 7 的日志记录：

```dbgcmd
0:000> !logexts.logc d 7
```

以下命令将启用 13 到 15 的类别的日志记录：

```dbgcmd
0:000> !logexts.logc e 13 15
```

以下命令将显示属于类别 3 的所有 Api:

```dbgcmd
0:000> !logexts.logc p 3
```

 

 





