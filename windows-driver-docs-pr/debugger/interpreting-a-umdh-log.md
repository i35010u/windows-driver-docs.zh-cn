---
title: 解释 UMDH 日志
description: 解释 UMDH 日志
ms.assetid: c5c74a3a-9598-4d89-8c5b-445138ae845f
keywords:
- UMDH，解释 UMDH 日志
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb576f15fd99bc8667b4b38c65a7a5cb674e8ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382706"
---
# <a name="interpreting-a-umdh-log"></a>解释 UMDH 日志


## <span id="ddk_interpreting_a_umdh_log_dtools"></span><span id="DDK_INTERPRETING_A_UMDH_LOG_DTOOLS"></span>


用户模式转储堆 (UMDH) 日志文件显示在进程中并且进行了分配了的堆栈的堆分配的列表。

此示例演示如何生成的日志，以具有 ID 1204 的流程。 日志将写入的文件 log1.txt。

```console
umdh -p:1204 -f:log1.txt
```

日志文件不可读，因为未解析符号。 UMDH 解析符号时分析日志。 此示例演示如何分析 log1.txt，并将结果存储在 result.txt。

```console
umdh -v log1.txt  > result.txt
```

## <a name="span-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>用于分析日志文件的符号文件


假设您有两台计算机：*记录计算机*创建 UMDH 日志以及一个*分析计算机*分析 UMDH 日志的位置。 分析计算机上的符号路径必须指向日志时间在加载日志记录计算机的 Windows 版本的符号。 未指向符号路径分析计算机上的符号服务器。 如果这样做，UMDH 将检索分析计算机运行的 Windows 版本的符号和 UMDH 将不会显示有意义的结果。

 

 





