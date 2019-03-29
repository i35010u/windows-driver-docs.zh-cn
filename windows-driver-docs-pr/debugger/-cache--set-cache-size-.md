---
title: .cache（设置缓存大小）
description: .Cache 命令设置用来保存从目标中获得的数据缓存的大小。 此外设置缓存和内存选项的数。
ms.assetid: 638cb2e6-b333-4311-967c-d86c2e93b4ec
keywords:
- .cache （设置缓存大小） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cache (Set Cache Size)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c7cac5f40151f3d11a1de2dbd04e7621863fc0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563121"
---
# <a name="cache-set-cache-size"></a>.cache（设置缓存大小）


**.Cache**命令设置用来保存从目标中获得的数据缓存的大小。 此外设置缓存和内存选项的数。

```dbgsyntax
.cache Size 
.cache Option 
.cache 
```

## <a name="span-idddkmetasetcachesizedbgspanspan-idddkmetasetcachesizedbgspanparameters"></a><span id="ddk_meta_set_cache_size_dbg"></span><span id="DDK_META_SET_CACHE_SIZE_DBG"></span>参数


<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
内核调试缓存，以千字节的大小。 如果*大小*为零，禁用缓存。 命令输出会显示以字节为单位的缓存大小。 （默认大小为 1000 KB）。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *选项*   
可以是下列选项之一：

<span id="hold"></span><span id="HOLD"></span>**hold**  
自动缓存刷新已禁用。

<span id="unhold"></span><span id="UNHOLD"></span>**unhold**  
关闭**保存**选项。 （这是默认设置。）

<span id="decodeptes"></span><span id="DECODEPTES"></span>**decodeptes**  
所有转换页表项 (Pte) 将都进行隐式解码。 （这是默认设置。）

<span id="nodecodeptes"></span><span id="NODECODEPTES"></span>**nodecodeptes**  
关闭**decodeptes**选项。

<span id="forcedecodeptes"></span><span id="FORCEDECODEPTES"></span>**forcedecodeptes**  
所有虚拟地址将转换为之前访问的物理地址。 此选项还会导致缓存被禁用。 除非您担心与内核模式内存，它是使用更加高效**forcedecodeuser**相反。

<span id="forcedecodeuser"></span><span id="FORCEDECODEUSER"></span>**forcedecodeuser**  
所有用户模式虚拟地址将都转换为之前访问的物理地址。 此选项还会导致缓存被禁用。

**请注意**  必须激活**forcedecodeuser** (或**forcedecodeptes**) 之前使用[ **.thread （设置注册上下文）** ](-thread--set-register-context-.md)， [ **.context （设置用户模式地址上下文）**](-context--set-user-mode-address-context-.md)， [ **.process （设置进程上下文）**](-process--set-process-context-.md)，或[ **！ 会话**](-session.md)期间实时调试。 如果您使用 **/p**选项与 **.thread**并 **.process**，则**forcedecodeuser**选项自动设置。 在任何其他情况下，你将需要使用 **.cache forcedecodeuser**显式命令。

 

<span id="noforcedecodeptes"></span><span id="NOFORCEDECODEPTES"></span>**noforcedecodeptes**  
关闭**forcedecodeptes**并**forcedecodeuser**选项。 （这是默认设置。）

<span id="flushall"></span><span id="FLUSHALL"></span>**flushall**  
删除整个虚拟内存缓存。

<span id="flushu"></span><span id="FLUSHU"></span>**flushu**  
删除所有项的范围，但从缓存中，出现错误，以及用户模式下的所有条目。

<span id="flush_Address"></span><span id="flush_address"></span><span id="FLUSH_ADDRESS"></span>**flush** *Address*  
删除缓存中，开始 4096 字节块*地址*。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
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

如果 **.cache**使用任何自变量、 当前缓存大小、 状态、 使用和显示选项。

**.Cache forcedecodeuser**或 **.cache forcedecodeptes**选项将仅上一次，只要调试器将继续分解为目标计算机。 如果任何单步执行或执行目标的发生， **noforcedecodeptes**状态将再次才会生效。 这可以防止调试器干扰执行或重新启动以用于生产的方式。

 

 





