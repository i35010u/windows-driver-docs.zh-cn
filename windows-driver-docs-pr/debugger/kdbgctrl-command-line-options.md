---
title: KDbgCtrl 命令行选项
description: KDbgCtrl 命令行使用以下语法
keywords:
- KDbgCtrl Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KDbgCtrl Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 299dc57e750c45762a33cdcd017cc15b1b8cf3b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801925"
---
# <a name="kdbgctrl-command-line-options"></a>KDbgCtrl 命令行选项


KDbgCtrl 命令行使用以下语法：

```dbgcmd
kdbgctrl [-e|-d|-c] [-ea|-da|-ca] [-eu|-du|-cu] [-eb|-db|-cb] [-sdb Size | -cdb] 

kdbgctrl -cx 

kdbgctrl -td ProcessID File 

kdbgctrl -sd {active|automatic|full|kernel|mini}

kdbgctrl -? 
```

## <a name="span-idddk_kdbgctrl_command_line_options_dbgspanspan-idddk_kdbgctrl_command_line_options_dbgspanparameters"></a><span id="ddk_kdbgctrl_command_line_options_dbg"></span><span id="DDK_KDBGCTRL_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-e______"></span><span id="_______-E______"></span>**-e**   
启用完全内核调试。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
禁用完全内核调试。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
检查是否已启用完全内核调试。 如果启用完整内核 Deubugging，则显示 true; 如果禁用完全内核调试，则显示 false。

<span id="_______-ea______"></span><span id="_______-EA______"></span>**-ea**   
启用自动内核调试。

<span id="_______-da______"></span><span id="_______-DA______"></span>**-da**   
禁用自动内核调试。

<span id="_______-ca______"></span><span id="_______-CA______"></span>**-ca**   
检查是否启用了自动内核调试。 如果启用了自动内核 Deubugging，则显示 true; 如果禁用自动内核调试，则显示 false。

<span id="_______-eu______"></span><span id="_______-EU______"></span>**-欧盟**   
启用 User-Mode 错误处理。

<span id="_______-du______"></span><span id="_______-DU______"></span>**-du**   
禁用 User-Mode 错误处理。

<span id="_______-cu______"></span><span id="_______-CU______"></span>**-cu**   
检查是否启用 User-Mode 错误处理。 如果启用 User-Mode 错误处理，则显示 true; 如果禁用 User-Mode 错误处理，则显示 false。

<span id="-eb"></span><span id="-EB"></span>**-eb**  
启用内核调试阻止。

<span id="-db"></span><span id="-DB"></span>**-db**  
禁止阻止内核调试

<span id="-cb"></span><span id="-CB"></span>**-cb**  
检查内核调试是否被阻止。 如果内核调试被阻止，则显示 true; 如果未阻止内核调试，则显示 false。

<span id="_______-sdb_______Size______"></span><span id="_______-sdb_______size______"></span><span id="_______-SDB_______SIZE______"></span>**-sdb** *大小*   
设置 DbgPrint 缓冲区的大小。 如果 *大小* 以 **0x** 为前缀，则将其解释为十六进制数。 如果前缀为 **0** (零) ，则将其解释为八进制。 否则，它将被解释为十进制。

<span id="_______-cdb______"></span><span id="_______-CDB______"></span>**-cdb**   
显示 DbgPrint 缓冲区的当前大小（以字节为单位）。

<span id="_______-cx______"></span><span id="_______-CX______"></span>**-cx**   
确定当前的完整内核调试设置并返回相应的值。 此选项不能与其他选项组合，且不会显示任何输出。 它设计为在批处理文件中使用，在该文件中可以测试 KDbgCtrl 程序的返回值。 可能的返回值如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>0x10001</strong></p></td>
<td align="left"><p>已启用完全内核调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0x10002</strong></p></td>
<td align="left"><p>已禁用完全内核调试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>任何其他值</p></td>
<td align="left"><p>出现了错误。 KDbgCtrl 无法确定完全内核调试的当前状态。</p></td>
</tr>
</tbody>
</table>

 

<span id="-td_ProcessID_File"></span><span id="-td_processid_file"></span><span id="-TD_PROCESSID_FILE"></span>**-td** *ProcessID* *文件*  
获取内核会审转储文件。 输入转储文件的进程 ID 和名称。

<span id="-sd_Type"></span>**-sd {active \| 自动 \| 完整 \| 内核 \| 迷你**   
设置要在发生系统崩溃时收集的转储类型，并重新加载故障转储堆栈。 有关转储类型的详细信息，请参阅多种 [Kernel-Mode 转储文件](varieties-of-kernel-mode-dump-files.md) 。

<span id="_______-_______"></span> **-?**   
显示 KDbgCtrl 的命令行帮助。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关所有 KDbgCtrl 设置的说明，请参阅 [使用 KDbgCtrl](using-kdbgctrl.md)。

 

 





