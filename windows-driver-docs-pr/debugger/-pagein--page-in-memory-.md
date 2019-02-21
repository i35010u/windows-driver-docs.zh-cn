---
title: .pagein （在内存中的页）
description: 中指定的内存区域的.pagein 命令页。
ms.assetid: 5fb8f9d2-d07a-49c3-b844-aade9bdba367
keywords:
- 页中内存 (.pagein) 命令
- 内存中，在内存页 (.pagein) 命令
- .pagein （页在内存中） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pagein (Page In Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b9f6f6126d3d0ff439bbfe212c6c431ab1476a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554994"
---
# <a name="pagein-page-in-memory"></a>.pagein （在内存中的页）


**.Pagein**命令中指定的内存区域的页。

```dbgcmd
.pagein [Options] Address
```

## <a name="span-idddkmetapageinmemorydbgspanspan-idddkmetapageinmemorydbgspanparameters"></a><span id="ddk_meta_page_in_memory_dbg"></span><span id="DDK_META_PAGE_IN_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下任意选项：

<span id="_p_Process"></span><span id="_p_process"></span><span id="_P_PROCESS"></span>**/p** **** *Process*  
指定拥有想要在页上的内存的进程的地址。 （更准确地说，此参数指定的进程的 EPROCESS 块的地址。）如果省略*进程*或指定设置的当前进程的零，调试器使用。 有关进程设置的详细信息，请参阅[ **.process （设置进程上下文）**](-process--set-process-context-.md)

<span id="_f"></span><span id="_F"></span>**/f**  
强制的内存分页中，即使该地址是在内核内存中和 Microsoft Windows 操作系统的版本不支持此操作。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定到页中的地址。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下 （但不是在本地内核调试）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

运行后 **.pagein**命令时，必须使用[ **g （转向）** ](g--go-.md)命令继续执行程序。 在很短的时间之后, 目标计算机自动进入调试器再次中断。

此时，你指定的地址中分页。 如果您使用 **/p**选项，进程上下文还设置为指定的进程，正如所用[ **.process /i 进程**](-process--set-process-context-.md)命令。

如果地址已在中，分页 **.pagein**命令仍要检查的地址中分页，然后重新进入调试器。 如果地址是无效的此命令仅返回到调试器会中断。

在 Windows Server 2003 和 Windows XP 中，您可以通过使用页仅使用用户模式地址 **.pagein**。 可以通过使用重写此限制 **/f**开关，但我们不建议使用此开关。 在 Windows Vista 中，您可以安全地页在用户模式和内核模式内存中。

**警告**  如果你使用 **.pagein**的 bug 检查可能会出现在 Windows Server 2003 或 Windows XP 中的内核堆栈中的地址上。

 

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
<td align="left"><p>支持 Windows XP 和更高版本的 Windows 中。</p></td>
</tr>
</tbody>
</table>

 

 





