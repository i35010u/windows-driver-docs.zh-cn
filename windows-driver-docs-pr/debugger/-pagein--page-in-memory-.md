---
title: .pagein（内存中的页面）
description: 指定内存区域中的 pagein 命令页。
keywords:
- " ( 中的页) 命令"
- 内存， ( 中的页) 命令
- pagein () Windows 调试中的内存页
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pagein (Page In Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf66115bcb65e0cb7594d674c5d32f710dad104f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837595"
---
# <a name="pagein-page-in-memory"></a>.pagein（内存中的页面）


指定内存区域中的 **pagein** 命令页。

```dbgcmd
.pagein [Options] Address
```

## <a name="span-idddk_meta_page_in_memory_dbgspanspan-idddk_meta_page_in_memory_dbgspanparameters"></a><span id="ddk_meta_page_in_memory_dbg"></span><span id="DDK_META_PAGE_IN_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下任意选项：

<span id="_p_Process"></span><span id="_p_process"></span><span id="_P_PROCESS"></span>**/p**  **** *处理*  
指定拥有要在其中分页的内存的进程的地址。 更准确地 (，此参数指定进程的 EPROCESS 块的地址。 ) 如果省略 " *处理* " 或指定零，则调试器将使用当前进程设置。 有关进程设置的详细信息，请参阅 [ **。进程 (设置进程上下文)**](-process--set-process-context-.md)

<span id="_f"></span><span id="_F"></span>**/f**  
强制将内存分页在中，即使地址在核心内存中并且 Microsoft Windows 操作系统的版本不支持此操作。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要在其中分页的地址。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅在本地内核调试期间 (内核模式) </p></td>
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

 

<a name="remarks"></a>备注
-------

运行 **pagein** 命令后，必须使用 [**g (中转)**](g--go-.md) 命令继续执行程序。 经过一段时间后，目标计算机会自动中断到调试器。

此时，你指定的地址将在中分页。 如果使用 **/p** 选项，则过程上下文也会设置为指定的进程，这与使用了 [**. process/i process**](-process--set-process-context-.md) 命令完全相同。

如果地址已在中分页，则 **pagein** 命令仍会检查地址是否已分页并返回到调试器。 如果地址无效，则此命令只会返回到调试器。

在 Windows Server 2003 和 Windows XP 中，你只能使用 **. pagein** 在用户模式地址中分页。 您可以使用 **/f** 开关覆盖此限制，但我们不建议使用此开关。 在 Windows Vista 中，可以安全地在用户模式和内核模式内存中页面。

**警告**   如果在 Windows Server 2003 或 Windows XP 中的内核堆栈中的地址上使用 **. pagein** ，则可能会发生 bug 检查。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中受支持。</p></td>
</tr>
</tbody>
</table>

 

 





