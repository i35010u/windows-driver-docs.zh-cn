---
title: .writemem（将内存写入文件）
description: Writemem 命令将部分内存写入文件。
keywords:
- writemem (将内存写入文件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .writemem (Write Memory to File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afb720ff0cbc29eae75252acd8ef331284793146
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814023"
---
# <a name="writemem-write-memory-to-file"></a>.writemem（将内存写入文件）


**Writemem** 命令将部分内存写入文件。

```dbgcmd
.writemem FileName Range 
```

## <a name="span-idddk_meta_write_memory_to_file_dbgspanspan-idddk_meta_write_memory_to_file_dbgspanparameters"></a><span id="ddk_meta_write_memory_to_file_dbg"></span><span id="DDK_META_WRITE_MEMORY_TO_FILE_DBG"></span>参数


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
指定要创建的文件的名称。 可以指定完整路径和文件名，也可以只指定文件名。 如果文件名包含空格，则 *文件名* 应括在引号中。 如果未指定路径，则使用当前目录。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要写入文件的内存范围。 有关语法的详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

内存按原义复制到文件。 不会以任何方式对其进行分析。

**Writemem** 命令与 [**. readmem ("从文件中读取内存)**](-readmem--read-memory-from-file-.md) " 命令。

 

 





