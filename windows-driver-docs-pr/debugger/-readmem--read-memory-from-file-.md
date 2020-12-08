---
title: .readmem（从文件读取内存）
description: Readmem 命令从指定的文件中读取原始二进制数据，并将数据复制到目标计算机的内存。
keywords:
- readmem (从文件) Windows 调试读取内存
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .readmem (Read Memory from File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb58463b0b3fc785160a06a2fe997384c55f9b73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837577"
---
# <a name="readmem-read-memory-from-file"></a>.readmem（从文件读取内存）


**Readmem** 命令从指定的文件中读取原始二进制数据，并将数据复制到目标计算机的内存。

```dbgcmd
.readmem FileName Range 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
指定要读取的文件的名称。 可以指定完整路径或仅指定文件名。 如果文件名包含空格，请将 *文件名* 用引号引起来。 如果未指定路径，则调试器将使用当前目录。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定用于将数据放置在内存中的地址范围。 此参数可以包含起始和结束地址，也可以包含起始地址和对象计数。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

内存数据按原义复制到目标计算机。 调试器不会以任何方式分析数据。 例如， **readmem myfile.txt 1000 10** 命令从 myfile.txt 文件复制10个字节，并将它们存储在目标计算机的内存中（从地址1000开始）。

**Readmem** 命令与 [**. Writemem (将内存写入文件)**](-writemem--write-memory-to-file-.md)命令。

 

 





