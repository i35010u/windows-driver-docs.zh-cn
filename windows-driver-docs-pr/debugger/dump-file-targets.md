---
title: 转储文件目标
description: 转储文件目标
ms.assetid: 83fb6753-a6c1-4899-9b06-a6331b3c31a8
keywords:
- 目标，转储文件
- 转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24846b3ae6bc7837f52917d697f3b8481e69f9a6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217382"
---
# <a name="dump-file-targets"></a>转储文件目标


## <span id="ddk_dump_file_targets_dbx"></span><span id="DDK_DUMP_FILE_TARGETS_DBX"></span>


有关故障转储文件的简介和概述，请参阅 [故障转储文件](crash-dump-files.md)。

### <a name="span-idopening_dump_filesspanspan-idopening_dump_filesspanspan-idopening_dump_filesspanopening-dump-files"></a><span id="Opening_Dump_Files"></span><span id="opening_dump_files"></span><span id="OPENING_DUMP_FILES"></span>打开转储文件

若要打开故障转储文件以用作调试程序目标，请使用 [**OpenDumpFile**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfile) 或 [**OpenDumpfileWide**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfilewide)。 这些方法类似于 [**opendump**](-opendump--open-dump-file-.md) 调试器命令。

**注意**   在调用[**WaitForEvent**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)方法之前，引擎不会完全附加到转储文件。 从进程或内核创建转储文件时，有关最后一个事件的信息存储在转储文件中。 打开转储文件后，下一次尝试执行时，引擎将为事件回调生成此事件。 只有在调试会话中才能使用转储文件。 有关更多详细信息，请参阅 [调试会话和执行模型](debugging-session-and-execution-model.md) 。

 

其他文件可用于帮助调试故障转储文件。 方法 [**AddDumpInformationFile**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfile) 和 [**AddDumpInformationFileWide**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfilewide) 注册文件，其中包含打开下一个转储文件时要使用的页面文件信息。 必须先调用这些方法，然后才能打开转储文件。 [**GetNumberDumpFiles**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberdumpfiles) 将返回打开当前转储文件时使用的此类文件数， [**GetDumpFile**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getdumpfile) 将返回这些文件的描述。

用户模式小型转储文件包含多个信息流。 可以使用 [**请求**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request) 操作 [**调试 \_ 请求 \_ 读取 \_ 用户 \_ 小型转储 \_ 流**](/previous-versions/ff541575(v=vs.85))来读取这些流。

### <a name="span-idcreating_dump_filesspanspan-idcreating_dump_filesspanspan-idcreating_dump_filesspancreating-dump-files"></a><span id="Creating_Dump_Files"></span><span id="creating_dump_files"></span><span id="CREATING_DUMP_FILES"></span>创建转储文件

若要创建当前目标（用户模式或内核模式）的故障转储文件，请使用 [**WriteDumpFile2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)。 此方法类似于 [**. dump**](-dump--create-dump-file-.md) 调试器命令。

 

