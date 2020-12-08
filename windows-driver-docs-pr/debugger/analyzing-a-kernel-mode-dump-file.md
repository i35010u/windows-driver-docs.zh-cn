---
title: 分析内核模式转储文件
description: 分析内核模式转储文件
keywords:
- 转储文件，分析内核模式转储文件
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3384e0114cad6fd66b32bdc5566097d5e7fc3cf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813315"
---
# <a name="analyzing-a-kernel-mode-dump-file"></a>分析内核模式转储文件

本节包括：

[使用 KD 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-kd.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="installing-symbol-files"></a>安装符号文件

无论使用哪种工具，都需要安装生成转储文件的 Windows 版本的符号文件。 选择用于分析转储文件的调试器将使用这些文件。 有关正确安装符号文件的详细信息，请参阅 [安装 Windows 符号文件](installing-windows-symbol-files.md)。

### <a name="dumpexam"></a>DumpExam

DumpExam 工具已过时。 在分析故障转储文件时不再需要它。
