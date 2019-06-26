---
title: 转储文件目标
description: 转储文件目标
ms.assetid: 83fb6753-a6c1-4899-9b06-a6331b3c31a8
keywords:
- 目标，转储文件
- 转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95d96f7a7548c5396c1180576cdd7c7f9b9af7a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361394"
---
# <a name="dump-file-targets"></a>转储文件目标


## <span id="ddk_dump_file_targets_dbx"></span><span id="DDK_DUMP_FILE_TARGETS_DBX"></span>


有关说明和故障转储文件的概述，请参阅[崩溃转储文件](crash-dump-files.md)。

### <a name="span-idopeningdumpfilesspanspan-idopeningdumpfilesspanspan-idopeningdumpfilesspanopening-dump-files"></a><span id="Opening_Dump_Files"></span><span id="opening_dump_files"></span><span id="OPENING_DUMP_FILES"></span>打开转储文件

若要打开用作调试器目标的崩溃转储文件，请使用[ **OpenDumpFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-opendumpfile)或[ **OpenDumpfileWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-opendumpfilewide)。 这些方法都是类似于[ **.opendump** ](-opendump--open-dump-file-.md)调试器命令。

**请注意**  引擎不会完全将附加到转储文件之前[ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)调用方法。 从进程或内核创建转储文件，最后一个事件的相关信息存储在转储文件。 打开转储文件后，尝试下一步的时间执行，该引擎将生成此事件的事件回调。 只有这样实际上已转储文件成为在调试会话中可用。 请参阅[调试会话和执行模型](debugging-session-and-execution-model.md)的更多详细信息。

 

可以使用其他文件，以帮助调试的崩溃转储文件。 方法[ **AddDumpInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfile)并[ **AddDumpInformationFileWide** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfilewide)注册包含页面文件信息的文件若要打开下一步的转储文件时使用。 打开转储文件之前，必须调用这些方法。 [**GetNumberDumpFiles** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberdumpfiles)将返回当前转储文件已打开时使用了此类文件的数目和[ **GetDumpFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getdumpfile)将返回它们的说明文件。

用户模式的小型转储文件包含多个流的信息。 这些流可以使用读取[**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**调试\_请求\_读取\_用户\_小型转储\_流**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))。

### <a name="span-idcreatingdumpfilesspanspan-idcreatingdumpfilesspanspan-idcreatingdumpfilesspancreating-dump-files"></a><span id="Creating_Dump_Files"></span><span id="creating_dump_files"></span><span id="CREATING_DUMP_FILES"></span>创建转储文件

若要创建的崩溃转储文件的当前目标-用户模式或内核模式-使用[ **WriteDumpFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)。 此方法是类似于[ **.dump** ](-dump--create-dump-file-.md)调试器命令。

 

 





