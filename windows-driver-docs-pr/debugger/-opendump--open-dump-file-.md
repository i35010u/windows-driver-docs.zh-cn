---
title: .opendump（打开转储文件）
description: Opendump 命令打开转储文件以进行调试。
keywords:
- opendump (打开) Windows 调试的转储文件
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .opendump (Open Dump File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 625d1ffad6e58a11f5b5bb81f22fbae90627db0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811279"
---
# <a name="opendump-open-dump-file"></a>.opendump（打开转储文件）


**Opendump** 命令打开转储文件以进行调试。

```dbgcmd
.opendump DumpFile 
.opendump /c "DumpFileInArchive" [CabFile] 
```

## <a name="span-idddk_meta_open_dump_file_dbgspanspan-idddk_meta_open_dump_file_dbgspanparameters"></a><span id="ddk_meta_open_dump_file_dbg"></span><span id="DDK_META_OPEN_DUMP_FILE_DBG"></span>参数


<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span>*DumpFile*   
指定要打开的转储文件的名称。 *DumpFile* 应包含文件扩展名 (通常为 dmp 或 .mdmp) 并且可以包含绝对路径或相对路径。 相对路径是相对于在其中启动调试器的目录的相对路径。

<span id="________c__DumpFileInArchive_"></span><span id="________c__dumpfileinarchive_"></span><span id="________C__DUMPFILEINARCHIVE_"></span>**/c** **"**<em>DumpFileInArchive</em>**"**  
指定要调试的转储文件的名称。 此转储文件必须包含在 *CabFile* 指定的存档文件中。 必须用引号将 *DumpFileInArchive* 文件引起来。

<span id="_______CabFile______"></span><span id="_______cabfile______"></span><span id="_______CABFILE______"></span>*CabFile*   
指定要打开的存档文件的名称。 *CabFile* 应包含文件扩展名 (通常是 .cab) 并且可以包含绝对路径或相对路径。 相对路径是相对于在其中启动调试器的目录的相对路径。 如果使用 **/c** 开关在存档中指定一个转储文件，但省略了 *CabFile*，则调试器将重复使用最近打开的存档文件。

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
<td align="left"><p>仅 (崩溃转储，但如果其他会话正在运行，则可以使用此命令) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 **opendump** 命令后，必须使用 [**g (中转)**](g--go-.md) 命令完成加载转储文件。

打开存档文件 (例如 CAB 文件) 时，应使用 **/c** 开关。 如果不使用此开关，并且为 *DumpFile* 指定了存档，则调试器将在此存档中打开具有 .mdmp 或 dmp 文件扩展名的第一个文件。

即使调试会话已在进行中，你也可以使用 **opendump** 。 此功能使你能够同时调试多个故障转储。 有关如何控制多目标会话的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

 
**注意**   在调试实时目标并将目标转储到一起时，有一些复杂的问题，因为每种调试类型的命令的行为有所不同。 例如，如果在当前系统为转储文件时使用 **g (中转)** 命令，则调试器将开始执行，但无法中断到调试器中，因为 break 命令未被识别为对转储文件调试无效。
 





