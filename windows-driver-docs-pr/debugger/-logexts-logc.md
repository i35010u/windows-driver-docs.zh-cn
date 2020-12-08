---
title: logexts.logc
description: Logexts. logc 扩展显示所有 API 类别、显示特定类别中的所有 Api，或启用和禁用一个或多个类别中的 Api 的日志记录。
keywords:
- logexts logc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04045baa962aac8dd29a83a8f7a9f7d76804d519
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828933"
---
# <a name="logextslogc"></a>!logexts.logc


**！ Logexts logc** 扩展显示所有 api 类别、显示特定类别中的所有 api，或启用和禁用一个或多个类别中的 api 的日志记录。

```dbgcmd
!logexts.logc e Categories 
!logexts.logc d Categories 
!logexts.logc p Category 
!logexts.logc 
```

## <a name="span-idddk__logexts_logc_dbgspanspan-idddk__logexts_logc_dbgspanparameters"></a><span id="ddk__logexts_logc_dbg"></span><span id="DDK__LOGEXTS_LOGC_DBG"></span>参数


<span id="_______e______"></span><span id="_______E______"></span>**e**   
启用指定类别的日志记录。

<span id="_______d______"></span><span id="_______D______"></span>**d**   
禁用指定类别的日志记录。

<span id="_______Categories______"></span><span id="_______categories______"></span><span id="_______CATEGORIES______"></span>*类别*   
指定要启用或禁用的类别。 如果列出了多个类别，请用空格分隔它们。 \*可以使用星号 () 来指示所有类别。

<span id="_______p______"></span><span id="_______P______"></span>**p**   
显示属于指定类别的所有 Api。

<span id="_______Category______"></span><span id="_______category______"></span><span id="_______CATEGORY______"></span>*类别*   
指定将显示其 Api 的类别。 只有一个类别可以与 **p** 选项一起指定。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [记录器和 LogViewer](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

如果没有任何选项， **！ logexts** 将显示当前可用类别列表，并指示已启用和已禁用的类别。

如果类别被禁用，则会删除该类别中所有 Api 的挂钩，因此不会再有任何性能开销。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

仅当你对程序具有 Windows (的特定类型的交互（例如，文件操作) ）感兴趣时，才启用特定类别会很有用。 这会减少日志文件的大小，还会减少记录器对进程执行速度产生的影响。

以下命令将启用所有类别的日志记录：

```dbgcmd
0:000> !logexts.logc e *
```

以下命令将禁用类别7的日志记录：

```dbgcmd
0:000> !logexts.logc d 7
```

以下命令将启用类别13和15的日志记录：

```dbgcmd
0:000> !logexts.logc e 13 15
```

以下命令将显示属于类别3的所有 Api：

```dbgcmd
0:000> !logexts.logc p 3
```

 

 





