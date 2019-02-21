---
title: .readmem （从文件读取内存）
description: .Readmem 命令从指定的文件中读取原始二进制数据，并将数据复制到目标计算机的内存。
ms.assetid: 128cbea1-5fb5-4685-8587-f814f94cc658
keywords:
- .readmem （从文件读取内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .readmem (Read Memory from File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2a23efb0889cccf1ab13cc167866222c4701306
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541429"
---
# <a name="readmem-read-memory-from-file"></a>.readmem （从文件读取内存）


**.Readmem**命令从指定的文件中读取原始二进制数据，并将数据复制到目标计算机的内存。

```dbgcmd
.readmem FileName Range 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
指定要读取的文件的名称。 您可以指定完整路径或文件名。 如果文件名包含空格，则将*文件名*引号引起来。 如果不指定路径，调试器将使用当前目录。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定将这些数据放在内存中的地址范围。 此参数可以包含起始和结束地址或起始地址和对象计数。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

 

<a name="remarks"></a>备注
-------

按原义的内存数据复制到目标计算机。 调试器不会分析以任何方式的数据。 例如， **.readmem myfile 1000 10**命令将从 Myfile 文件复制 10 个字节，并将其存储在目标计算机的内存中，地址 1000年开始。

**.Readmem**命令与相反[ **.writemem （到文件写入内存）** ](-writemem--write-memory-to-file-.md)命令。

 

 





