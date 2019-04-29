---
title: KDbgCtrl 命令行选项
description: KDbgCtrl 命令行使用以下语法
ms.assetid: 0367a09d-c475-4aeb-8f88-47d51ec7e9d5
keywords:
- KDbgCtrl 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KDbgCtrl Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 49569683160f426e7b2b3ad113ebd3528b2735ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367211"
---
# <a name="kdbgctrl-command-line-options"></a>KDbgCtrl 命令行选项


KDbgCtrl 命令行使用以下语法：

```dbgcmd
kdbgctrl [-e|-d|-c] [-ea|-da|-ca] [-eu|-du|-cu] [-eb|-db|-cb] [-sdb Size | -cdb] 

kdbgctrl -cx 

kdbgctrl -td ProcessID File 

kdbgctrl -? 
```

## <a name="span-idddkkdbgctrlcommandlineoptionsdbgspanspan-idddkkdbgctrlcommandlineoptionsdbgspanparameters"></a><span id="ddk_kdbgctrl_command_line_options_dbg"></span><span id="DDK_KDBGCTRL_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
启用完整的内核调试。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
禁用完整的内核调试。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
检查是否启用了完整的内核调试。 如果完整内核 Deubugging 已启用，并且如果完整的内核调试处于禁用状态，则显示 false，则显示 true。

<span id="_______-ea______"></span><span id="_______-EA______"></span> **-ea**   
启用自动内核调试。

<span id="_______-da______"></span><span id="_______-DA______"></span> **-da**   
禁用自动内核调试。

<span id="_______-ca______"></span><span id="_______-CA______"></span> **-ca**   
检查是否启用了自动内核调试。 如果自动内核 Deubugging 已启用，并且如果禁用自动内核调试，则显示 false，则显示 true。

<span id="_______-eu______"></span><span id="_______-EU______"></span> **-eu**   
使用户模式下的错误处理。

<span id="_______-du______"></span><span id="_______-DU______"></span> **-du**   
禁用用户模式下的错误处理。

<span id="_______-cu______"></span><span id="_______-CU______"></span> **-cu**   
检查是否启用了用户模式下的错误处理。 如果用户模式下的错误处理已启用，并且如果用户模式下的错误处理处于禁用状态，则显示 false，则显示 true。

<span id="-eb"></span><span id="-EB"></span>**-eb**  
启用阻塞的内核调试。

<span id="-db"></span><span id="-DB"></span>**-db**  
禁用阻塞的内核调试

<span id="-cb"></span><span id="-CB"></span>**-cb**  
检查是否阻止内核调试。 如果内核调试被阻止，并且如果内核调试未被阻止，则显示 false，则显示 true。

<span id="_______-sdb_______Size______"></span><span id="_______-sdb_______size______"></span><span id="_______-SDB_______SIZE______"></span> **-sdb** *Size*   
设置 DbgPrint 缓冲区的大小。 如果*大小*带有前缀**0x**它将被解释为十六进制数。 如果将使用前缀**0** （零），它将被解释为八进制数值。 否则，它将解释为十进制。

<span id="_______-cdb______"></span><span id="_______-CDB______"></span> **-cdb**   
显示当前大小，以字节为单位的 DbgPrint 缓冲区。

<span id="_______-cx______"></span><span id="_______-CX______"></span> **-cx**   
确定完整的内核调试的当前设置并返回适当的值。 此选项不能结合其他选项，并不会显示任何输出。 它专为在批处理文件可以在何处测试 KDbgCtrl 程序的返回值中使用。 可能的返回值如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>0x10001</strong></p></td>
<td align="left"><p>启用完整的内核调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0x10002</strong></p></td>
<td align="left"><p>完整的内核调试已禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>任何其他值</p></td>
<td align="left"><p>发生错误。 KDbgCtrl 无法确定完整的内核调试的当前状态。</p></td>
</tr>
</tbody>
</table>

 

<span id="-td_ProcessID_File"></span><span id="-td_processid_file"></span><span id="-TD_PROCESSID_FILE"></span>**-td** *ProcessID* *File*  
获取内核会审转储文件。 输入的进程 ID 和转储文件的名称。

<span id="_______-_______"></span> **-?**   
显示命令行帮助 KDbgCtrl。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关所有 KDbgCtrl 设置的说明，请参阅[使用 KDbgCtrl](using-kdbgctrl.md)。

 

 





