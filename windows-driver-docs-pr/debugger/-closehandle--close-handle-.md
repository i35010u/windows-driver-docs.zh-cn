---
title: .closehandle（关闭句柄）
description: Closehandle 命令关闭目标应用程序拥有的句柄。
keywords:
- closehandle (关闭句柄) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .closehandle (Close Handle)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d8db653deb58c578afd120ff1f071a5ba1d2a08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795745"
---
# <a name="closehandle-close-handle"></a>.closehandle（关闭句柄）


**Closehandle** 命令关闭目标应用程序拥有的句柄。

```dbgsyntax
.closehandle Handle 
.closehandle -a 
```

## <a name="span-idddk_meta_close_handle_dbgspanspan-idddk_meta_close_handle_dbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
指定要关闭的句柄。

<span id="_______-a______"></span><span id="_______-A______"></span>**-a**   
导致关闭目标应用程序所拥有的所有句柄。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您可以使用 [**！ handle**](-handle.md) 扩展显示现有句柄。

 

 





