---
title: 解释 UMDH 日志
description: 解释 UMDH 日志
keywords:
- UMDH，解释 UMDH 日志
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4318bdb6468efd480703d41d3b39626b5c45ebe7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801957"
---
# <a name="interpreting-a-umdh-log"></a>解释 UMDH 日志


## <span id="ddk_interpreting_a_umdh_log_dtools"></span><span id="DDK_INTERPRETING_A_UMDH_LOG_DTOOLS"></span>


User-Mode 转储堆 (UMDH) 日志文件显示进程中的堆分配列表和进行分配的堆栈。

此示例演示如何为 ID 为1204的进程生成日志。 日志将写入 log1.txt 文件中。

```console
umdh -p:1204 -f:log1.txt
```

由于未解析符号，因此无法读取日志文件。 分析日志时，UMDH 解析符号。 此示例演示如何分析 log1.txt 并将结果存储在 result.txt 中。

```console
umdh -v log1.txt  > result.txt
```

## <a name="span-idsymbol_files_for_analyzing_a_log_filespanspan-idsymbol_files_for_analyzing_a_log_filespanspan-idsymbol_files_for_analyzing_a_log_filespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>用于分析日志文件的符号文件


假设您有两台计算机：一 *台日志记录计算机* ，您可以在其中创建 UMDH 日志以及分析 UMDH 日志的 *分析计算机* 。 分析计算机上的符号路径必须指向在日志记录时日志记录计算机上加载的 Windows 版本的符号。 不要将分析计算机上的符号路径指向符号服务器。 如果这样做，UMDH 将检索分析计算机上运行的 Windows 版本的符号，UMDH 将不会显示有意义的结果。

 

 





