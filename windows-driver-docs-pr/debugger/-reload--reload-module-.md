---
title: .reload（重新加载模块）
description: Reload.sql 命令删除指定模块的所有符号信息, 并根据需要重新加载这些符号。 在某些情况下, 此命令还会重新加载或卸载模块本身。
ms.assetid: 750eb1a2-7af9-4f2d-81ca-9ea0fb157961
keywords:
- 重载模块 (reload.sql) 命令
- 符号, 重装模块 (reload.sql) 命令
- 。重装 (重新加载模块) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .reload (Reload Module)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 610f495e4b7e77307a9a01f796608e272f64e0fc
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063891"
---
# <a name="reload-reload-module"></a>.reload（重新加载模块）


**Reload.sql**命令删除指定模块的所有符号信息, 并根据需要重新加载这些符号。 在某些情况下, 此命令还会重新加载或卸载模块本身。

```dbgcmd
.reload [Options] [Module[=Address[,Size[,Timestamp]]]] 
.reload -?
```

## <a name="span-idddk_meta_reload_module_dbgspanspan-idddk_meta_reload_module_dbgspanparameters"></a><span id="ddk_meta_reload_module_dbg"></span><span id="DDK_META_RELOAD_MODULE_DBG"></span>Parameters


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下任意选项:

<span id="_d"></span><span id="_D"></span> **/d**  
重载调试器的模块列表中的所有模块。 (如果省略所有参数, 则在用户模式调试过程中, 这种情况是默认情况。)

<span id="_f"></span><span id="_F"></span> **/f**  
强制调试器立即加载符号。 此参数将重写*延迟符号加载*。 有关详细信息, 请参阅下面的 "备注" 部分。

<span id="_i"></span><span id="_I"></span> **/i**  
忽略 .pdb 文件版本中的不匹配。 (如果不包含此参数, 则调试器不会加载不匹配的符号文件。)当你使用 **/i**时, 还会使用 **/f** , 即使你未显式指定它。

<span id="_l"></span><span id="_L"></span> **/l**  
列出了模块, 但不会重新加载其符号。 (在内核模式下, 此参数提供类似于[**lm**](lm--list-loaded-modules-.md)命令的输出。)

<span id="_n"></span><span id="_N"></span> **/n**  
仅重新加载内核符号。 此参数不会重新加载任何用户符号。 (只能在内核模式调试过程中使用此选项。)

<span id="_o"></span><span id="_O"></span> **/o**  
强制覆盖符号服务器的下游存储区中的缓存文件。 使用此标志时, 还应包括 **/f**。 默认情况下, 不会覆盖下游存储区文件。

由于符号服务器对二进制文件的每个不同版本的符号使用不同的文件名, 因此不必使用此选项, 除非你认为下游存储已损坏。

<span id="_s"></span><span id="_S"></span> **/s**  
重新加载系统的模块映像列表中的所有模块。 (省略所有参数时, 在内核模式调试过程中, 这种情况是默认情况。)

如果在执行用户模式调试时按名称加载单个系统模块, 则必须包括 **/s**。

<span id="_u"></span><span id="_U"></span> **/u**  
卸载指定的模块及其所有符号。 调试器卸载其名称与*模块*匹配的所有已加载模块, 而不考虑完整路径。 还搜索映像名称。 有关详细信息, 请参阅以下 "备注" 部分中的说明。

<span id="_unl"></span><span id="_UNL"></span> **/unl**  
基于卸载的模块列表中的图像信息重新加载符号。

<span id="_user"></span><span id="_USER"></span> **/user**  
仅重新加载用户符号。 (只能在内核模式调试过程中使用此选项。)

<span id="_v"></span><span id="_V"></span> **/v**  
启用详细模式。

<span id="_w"></span><span id="_W"></span> **/w**  
将*模块*视为文本字符串。 此处理会阻止调试器扩展通配符。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定目标系统上要在主计算机上重新加载符号的映像的名称。 *模块*应包含文件的名称和文件扩展名。 除非使用 **/w**选项, 否则*模块*可能包含各种通配符和说明符。 有关语法的详细信息, 请参阅[字符串通配符语法](string-wildcard-syntax.md)。 如果省略*Module*, 则**reload.sql**命令的行为取决于你使用的*选项*。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定模块的基址。 通常, 仅当图像标头已损坏或被分页时, 才需要使用此地址。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
指定模块映像的大小。 在许多情况下, 调试器知道了模块的正确大小。 调试器不知道正确的大小时, 应指定*size*。 此大小可以是实际的模块大小或更大的数字, 但大小不应为较小的数字。 通常, 仅当图像标头已损坏或被分页时, 才需要使用此大小。

<span id="_______Timestamp______"></span><span id="_______timestamp______"></span><span id="_______TIMESTAMP______"></span>*Timestamp*   
指定模块映像的时间戳。 在许多情况下, 调试器知道模块的正确时间戳。 调试器不知道时间戳时, 应指定*时间戳*。 通常, 仅当图像标头已损坏或被分页时, 才需要具有此时间戳。

**注意**地址、大小和时间戳参数之间必须没有空格。  

 

<span id="_______-_______"></span> **-?**    
显示此命令的简短帮助文本。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式, 内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时, 故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关延迟 (懒惰) 符号加载的详细信息, 请参阅[延迟符号加载](deferred-symbol-loading.md)。 有关其他符号选项的详细信息, 请参阅[设置符号选项](symbol-options.md)。

<a name="remarks"></a>备注
-------

**Reload.sql**命令不会导致符号信息被读取。 相反, 此命令使调试器知道符号文件可能已更改, 或者应将新模块添加到模块列表中。 此命令会使调试器修订其模块列表并删除指定模块的符号信息。 在需要信息之前, 不会从各个 .pdb 文件中读取实际的符号信息。 (这种加载称为*延迟符号加载*或*延迟的符号加载*。)

您可以通过使用 **/f**选项或通过发出[**Ld (加载符号)** ](ld--load-symbols-.md)命令强制进行符号加载。

如果系统停止响应 (即系统崩溃), 则**reload.sql**命令非常有用, 这可能会导致丢失要调试的目标计算机的符号。 如果已更新符号树, 此命令也会很有用。

如果由于某种原因 (例如, 正在卸载的模块或已分页出) 图像标头不正确, 则可以通过使用 **/unl**参数或同时指定*地址*和*大小*来正确加载符号。

**Reload.sql/u**命令执行广泛的搜索。 调试器首先尝试将*模块*与确切的模块名称匹配, 而不考虑路径。 如果调试器找不到此匹配项,*模块*将被视为加载的映像的名称。 例如, 如果驻留在内存中的 HAL 的模块名称为 halacpi, 则以下两个命令都将卸载其符号。

```dbgcmd
kd> .reload /u halacpi.dll

kd> .reload /u hal
```

如果要执行用户模式调试, 并想要加载不是目标应用程序的模块列表一部分的模块, 则必须包括 **/s**选项, 如下面的示例所示。

```dbgcmd
0:000> .reload /u ntdll.dll
Unloaded ntdll.dll

0:000> .reload /s /f ntdll.dll
```

 

 





