---
title: .opendump （打开转储文件）
description: .Opendump 命令将打开转储文件以进行调试。
ms.assetid: 751af9ea-be7e-4aef-a6f6-fc99e3b3a56e
keywords:
- .opendump （打开转储文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .opendump (Open Dump File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 820a38241bfc83ea1a8929132da3298cdd77eeb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544158"
---
# <a name="opendump-open-dump-file"></a>.opendump （打开转储文件）


**.Opendump**命令将打开转储文件以进行调试。

```dbgcmd
.opendump DumpFile 
.opendump /c "DumpFileInArchive" [CabFile] 
```

## <a name="span-idddkmetaopendumpfiledbgspanspan-idddkmetaopendumpfiledbgspanparameters"></a><span id="ddk_meta_open_dump_file_dbg"></span><span id="DDK_META_OPEN_DUMP_FILE_DBG"></span>参数


<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span> *DumpFile*   
指定要打开的转储文件的名称。 *DumpFile*应包括文件扩展名 （通常.dmp 或.mdmp） 并且可以包括绝对或相对路径。 相对路径是相对于目录中启动调试器。

<span id="________c__DumpFileInArchive_"></span><span id="________c__dumpfileinarchive_"></span><span id="________C__DUMPFILEINARCHIVE_"></span> **/c** **"**<em>DumpFileInArchive</em>**"**  
指定要调试转储文件的名称。 此转储文件必须包含在存档文件*CabFile*指定。 必须将*DumpFileInArchive*在引号中的文件。

<span id="_______CabFile______"></span><span id="_______cabfile______"></span><span id="_______CABFILE______"></span> *CabFile*   
指定要打开的存档文件的名称。 *CabFile*应包括文件扩展名 (通常.cab) 并且可以包括绝对或相对路径。 相对路径是相对于目录中启动调试器。 如果您使用 **/c**切换在存档中指定的转储文件，但省略*CabFile*，调试器会重用最近打开的存档文件。

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
<td align="left"><p>崩溃转储仅 （但如果其他会话正在运行，可以使用此命令）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在使用后 **.opendump**命令时，必须使用[ **g （转向）** ](g--go-.md)命令完成加载转储文件。

如果打开的存档文件 （如 CAB 文件），则应使用 **/c**切换。 如果不使用此开关并指定存档中的以进行*DumpFile*，调试器将打开扩展名为.mdmp 或.dmp 文件在该存档文件中的第一个文件。

可以使用 **.opendump**即使调试会话已经正在进行中。 此功能，可同时调试多个故障转储。 有关如何控制多个目标会话的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

 
**请注意**  有采用十分复杂，在调试实时目标和转储目标组合在一起，因为每种类型的调试方式不同命令的行为时。 例如，如果您使用**g （转向）** 命令时当前系统是转储文件，调试器开始执行，但不是能中断返回到调试器，因为换行命令无法识别为有效的调试转储文件。
 





