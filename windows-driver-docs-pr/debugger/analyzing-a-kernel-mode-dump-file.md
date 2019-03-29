---
title: 分析内核模式转储文件
description: 分析内核模式转储文件
ms.assetid: 2bda51c2-b022-4740-8df9-5a2cf2382e3e
keywords:
- 转储文件，分析内核模式转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af1c6b4306b919504ec2aec70a5c1a9a28e03d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563566"
---
# <a name="analyzing-a-kernel-mode-dump-file"></a>分析内核模式转储文件


## <span id="ddk_analyzing_a_kernel_mode_dump_file_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


本部分包括：

[分析具有 KD 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-kd.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[分析具有 KAnalyze 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-kanalyze.md)

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>安装符号文件

无论所使用的工具，您需要安装生成转储文件的 Windows 版本的符号文件。 选择要用于分析转储文件调试程序将使用这些文件。 有关符号文件的正确安装的详细信息，请参阅[安装 Windows 符号文件](installing-windows-symbol-files.md)。

### <a name="span-idddkdumpexamdbgspanspan-idddkdumpexamdbgspandumpexam"></a><span id="ddk_dumpexam_dbg"></span><span id="DDK_DUMPEXAM_DBG"></span>DumpExam

DumpExam 工具已过时。 它不再需要在分析故障转储文件中。

 

 





