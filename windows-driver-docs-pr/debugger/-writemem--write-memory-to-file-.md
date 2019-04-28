---
title: .writemem（将内存写入文件）
description: .Writemem 命令向文件写入内存的一部分。
ms.assetid: 928e9452-d9b4-49fa-a5fa-cdc3832d7349
keywords:
- .writemem （到文件写入内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .writemem (Write Memory to File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed5a669a39292388e96294742b9f7749516f03f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348033"
---
# <a name="writemem-write-memory-to-file"></a>.writemem（将内存写入文件）


**.Writemem**命令向文件写入内存的一部分。

```dbgcmd
.writemem FileName Range 
```

## <a name="span-idddkmetawritememorytofiledbgspanspan-idddkmetawritememorytofiledbgspanparameters"></a><span id="ddk_meta_write_memory_to_file_dbg"></span><span id="DDK_META_WRITE_MEMORY_TO_FILE_DBG"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
指定要创建的文件的名称。 您可以指定完整路径和文件名或只是文件名称。 如果文件名称包含空格，则*文件名*应括在引号中。 如果未指定路径，则使用当前目录。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定要写入到文件的内存范围。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

内存是按字面意思复制到文件。 它不是以任何方式进行分析。

**.Writemem**命令与相反[ **.readmem （从文件读取内存）** ](-readmem--read-memory-from-file-.md)命令。

 

 





