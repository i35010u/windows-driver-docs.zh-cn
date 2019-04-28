---
title: .reload（重新加载模块）
description: .Reload 命令删除指定的模块的所有符号信息，并根据需要重新加载这些符号。 在某些情况下，此命令还将重新加载或卸载该模块本身。
ms.assetid: 750eb1a2-7af9-4f2d-81ca-9ea0fb157961
keywords:
- 重新加载模块 (.reload) 命令
- 符号，重新加载模块 (.reload) 命令
- .reload （重新加载模块） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .reload (Reload Module)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36c3aba41ef95f9880ba5e1835c1b6a1392c069b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335739"
---
# <a name="reload-reload-module"></a>.reload（重新加载模块）


**.Reload**命令删除指定的模块的所有符号信息，并根据需要重新加载这些符号。 在某些情况下，此命令还将重新加载或卸载该模块本身。

```dbgcmd
.reload [Options] [Module[=Address[,Size[,Timestamp]]]] 
.reload -?
```

## <a name="span-idddkmetareloadmoduledbgspanspan-idddkmetareloadmoduledbgspanparameters"></a><span id="ddk_meta_reload_module_dbg"></span><span id="DDK_META_RELOAD_MODULE_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下任意选项：

<span id="_d"></span><span id="_D"></span>**/d**  
重新加载所有模块的调试程序的模块列表中。 （时忽略所有参数，这种情况下是默认值在用户模式下调试过程。）

<span id="_f"></span><span id="_F"></span>**/f**  
强制调试器立即加载符号。 此参数重写*延迟符号加载*。 有关详细信息，请参阅以下备注部分。

<span id="_i"></span><span id="_I"></span>**/i**  
将忽略.pdb 文件版本不匹配。 （如果未包括此参数，调试器不会不会加载不匹配的符号文件。）当你使用 **/i**， **/f**此外，即使未显式指定它使用。

<span id="_l"></span><span id="_L"></span>**/l**  
列出的模块，但不重新加载其符号。 (在内核模式下，该参数提供了相同的输出[ **！ 驱动程序**](-drivers.md)扩展。)

<span id="_n"></span><span id="_N"></span>**/n**  
重新加载内核的符号。 此参数不会重新加载任何用户符号。 （可以使用此选项仅在内核模式调试。）

<span id="_o"></span><span id="_O"></span>**/o**  
强制符号服务器的下游存储覆盖中缓存的文件。 当使用此标志时，还应包括 **/f**。 默认情况下，将永远不会覆盖下游存储文件。

由于符号服务器使用的每个不同的内部版本的二进制文件的符号的独立的文件名称，因此你无需使用此选项，除非你认为你的下游存储已损坏。

<span id="_s"></span><span id="_S"></span>**/s**  
重新加载系统的模块映像列表中的所有模块。 （时忽略所有参数，这种情况下是默认值在内核模式调试过程。）

如果要按名称加载各个系统模块在执行用户模式下调试时，必须包括 **/s**。

<span id="_u"></span><span id="_U"></span>**/u**  
卸载指定的模块和所有符号。 调试器将卸载任何加载的模块，其名称与匹配*模块*，无论的完整路径。 此外可搜索图像名称。 有关详细信息，请参阅以下备注部分中的说明。

<span id="_unl"></span><span id="_UNL"></span>**/unl**  
重新加载基于图像信息在卸载的模块列表中的符号。

<span id="_user"></span><span id="_USER"></span>**/user**  
仅用户符号将重新加载。 （可以使用此选项仅在内核模式调试。）

<span id="_v"></span><span id="_V"></span>**/v**  
开启详细模式。

<span id="_w"></span><span id="_W"></span>**/w**  
将视为*模块*作为文字字符串。 此种处理方式使调试器无法展开通配符字符。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定要为其重新加载在主计算机上的符号在目标系统上的图像的名称。 *模块*应包括文件的名称和文件扩展名。 除非使用 **/w**选项，*模块*可能包含多个通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。 如果省略*模块*的行为 **.reload**命令取决于其*选项*你使用。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定模块的基址。 通常情况下，您一定映像标头已损坏或换出时才需要此地址。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
指定的模块映像的大小。 在许多情况下，调试器知道该模块的正确大小。 当调试器不知道正确的大小时，则应指定*大小*。 此大小可以是实际模块大小或较大，但大小不应为较小的数字。 通常情况下，您一定映像标头已损坏或换出时才需要此大小。

<span id="_______Timestamp______"></span><span id="_______timestamp______"></span><span id="_______TIMESTAMP______"></span> *时间戳*   
指定模块映像的时间的戳。 在许多情况下，调试器知道该模块的正确时间戳。 当调试器不知道时间戳时，则应指定*时间戳*。 通常情况下，您一定映像标头已损坏或换出时才需要此时间戳。

**请注意**  必须之间没有空白空格*地址*，*大小*，以及*时间戳*参数。

 

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关延迟 （延迟） 符号加载详细信息，请参阅[推迟符号加载](deferred-symbol-loading.md)。 有关其他符号选项的详细信息，请参阅[设置符号选项](symbol-options.md)。

<a name="remarks"></a>备注
-------

**.Reload**命令不会导致要读取的符号信息。 相反，此命令使调试器了解符号文件可能已更改，或者应将新模块添加到模块列表。 此命令将导致调试器修改其模块列表，并删除其为指定的模块的符号信息。 之前所需的信息是从单个.pdb 文件不读取的实际符号信息。 (这种加载名为*延迟符号加载*或*延迟的符号加载*。)

您可以强制符号加载，若要通过使用会发生 **/f**选项，或通过发出[ **ld （加载符号）** ](ld--load-symbols-.md)命令。

**.Reload**命令很有用，如果系统停止响应 （即，崩溃），这可能导致丢失正在调试的目标计算机的符号。 该命令也可以是已更新的符号树的情况下很有用。

如果映像标头不正确出于某种原因，如正在卸载模块或换出时，您可以通过使用正确加载符号 **/unl**自变量，或指定这两个*地址*并*大小*。

**.Reload /u**命令执行广泛的搜索。 调试器首先尝试匹配*模块*替换为确切的模块名称，而不考虑路径。 如果调试器无法找到此匹配项，*模块*视为已加载的映像的名称。 例如，如果在内存中驻留的 HAL halacpi.dll 的模块名称，这两个以下的命令卸载其符号。

```dbgcmd
kd> .reload /u halacpi.dll

kd> .reload /u hal
```

如果正在执行用户模式下调试，想要加载的模块，不是目标应用程序的模块列表的一部分，必须包括 **/s**选项，如以下示例所示。

```dbgcmd
0:000> .reload /u ntdll.dll
Unloaded ntdll.dll

0:000> .reload /s /f ntdll.dll
```

 

 





