---
title: .cache（设置缓存大小）
description: Cache 命令设置用于保存从目标获取的数据的缓存大小。 还设置了一些缓存和内存选项。
keywords:
- 。缓存 (设置缓存大小) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cache (Set Cache Size)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 32f0d5b990c3242ab017b4fae0a3b33ed30af3b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814109"
---
# <a name="cache-set-cache-size"></a>.cache（设置缓存大小）


**Cache** 命令设置用于保存从目标获取的数据的缓存大小。 还设置了一些缓存和内存选项。

```dbgsyntax
.cache Size 
.cache Option 
.cache 
```

## <a name="span-idddk_meta_set_cache_size_dbgspanspan-idddk_meta_set_cache_size_dbgspanparameters"></a><span id="ddk_meta_set_cache_size_dbg"></span><span id="DDK_META_SET_CACHE_SIZE_DBG"></span>参数


<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
内核调试缓存的大小（kb）。 如果 *大小* 为零，则将禁用缓存。 命令输出显示缓存大小（以字节为单位）。  (默认大小为 1000 KB。 ) 

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项*   
可以是下列选项之一：

<span id="hold"></span><span id="HOLD"></span>**暂时**  
已禁用自动缓存刷新。

<span id="unhold"></span><span id="UNHOLD"></span>**unhold**  
关闭 **保留** 选项。 （这是默认设置。）

<span id="decodeptes"></span><span id="DECODEPTES"></span>**decodeptes**  
将隐式解码 (Pte) 的所有转换页表项。 （这是默认设置。）

<span id="nodecodeptes"></span><span id="NODECODEPTES"></span>**nodecodeptes**  
关闭 **decodeptes** 选项。

<span id="forcedecodeptes"></span><span id="FORCEDECODEPTES"></span>**forcedecodeptes**  
在访问之前，所有虚拟地址都将转换为物理地址。 此选项还会导致缓存被禁用。 除非你担心内核模式内存，否则使用 **forcedecodeuser** 更有效。

<span id="forcedecodeuser"></span><span id="FORCEDECODEUSER"></span>**forcedecodeuser**  
在访问之前，所有的用户模式虚拟地址都将转换为物理地址。 此选项还会导致缓存被禁用。

**注意**   在使用) 之前，必须激活 **forcedecodeuser** (或 **forcedecodeptes** 。 [**(设置寄存器上下文)**](-thread--set-register-context-.md)， [**上下文 (设置 User-Mode 地址上下文**](-context--set-user-mode-address-context-.md)) ，在实时调试期间 [**处理 (设置进程上下文)**](-process--set-process-context-.md)或 [**！ session**](-session.md) 。 如果将 **/p** 选项与 **thread** 和 **. 进程** 一起使用，则会自动设置 **forcedecodeuser** 选项。 在任何其他情况下，都需要显式使用 " **forcedecodeuser** " 命令。

 

<span id="noforcedecodeptes"></span><span id="NOFORCEDECODEPTES"></span>**noforcedecodeptes**  
禁用 **forcedecodeptes** 和 **forcedecodeuser** 选项。 （这是默认设置。）

<span id="flushall"></span><span id="FLUSHALL"></span>**flushall**  
删除整个虚拟内存缓存。

<span id="flushu"></span><span id="FLUSHU"></span>**flushu**  
从缓存中删除具有错误的范围的所有条目，以及所有用户模式条目。

<span id="flush_Address"></span><span id="flush_address"></span><span id="FLUSH_ADDRESS"></span>**刷新***地址*  
从 *地址* 开始删除缓存的4096字节块。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
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

如果在没有参数的情况下使用 **缓存** ，则显示当前缓存大小、状态和选项。

仅当调试器保持在目标计算机中时，才会持续执行 **cache forcedecodeuser** 或 **cache forcedecodeptes** 选项。 如果发生了目标的任何单步执行或执行，则 **noforcedecodeptes** 状态将再次生效。 这会阻止调试器干扰执行或重新启动产生效益等待。

 

 





