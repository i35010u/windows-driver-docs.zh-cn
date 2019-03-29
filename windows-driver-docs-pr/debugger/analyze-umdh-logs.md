---
title: 分析 UMDH 日志
description: 使用以下命令，以分析通过运行 UMDH 语法创建的用户模式转储堆 (UMDH) 日志中所述分析运行中的进程。
ms.assetid: 66e559b2-0335-4a1d-ba6c-dde6b826dc5f
keywords:
- 分析 UMDH 日志 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Analyze UMDH Logs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3300e26ed433a558d2590c973d67501bf4276731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564259"
---
# <a name="analyze-umdh-logs"></a>分析 UMDH 日志


使用以下命令来分析用户模式转储堆 (UMDH) 日志创建的运行中所述的语法与 UMDH [**分析运行中的进程**](analyze-a-running-process.md)。 此分析专注于分配，而不是堆栈跟踪。

可以分析单个日志文件，也可以比较不同的运行中的程序或驱动程序的内存转储分配随着时间的推移检测所做的更改的日志。

```dbgcmd
umdh [-d] [-v] [-l] File1 [File2] [-h | ?]
```

## <a name="span-idddkanalyzeumdhlogsdtoolsspanspan-idddkanalyzeumdhlogsdtoolsspanparameters"></a><span id="ddk_analyze_umdh_logs_dtools"></span><span id="DDK_ANALYZE_UMDH_LOGS_DTOOLS"></span>参数


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
十进制数字中显示数值数据。 默认值为十六进制。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
详细模式。 包括跟踪，以及摘要信息。 分析单个日志文件时，跟踪是最有帮助。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
在日志中包含文件的名称和行号。 （请注意，参数是小写的字母"L"(这是不是第一个。）

<span id="_______File1__File2_"></span><span id="_______file1__file2_"></span><span id="_______FILE1__FILE2_"></span> *File1* \[*File2*\]  
指定要分析的 UMDH 日志文件。

UMDH 创建日志文件中运行时[**分析正在运行的进程**](analyze-a-running-process.md)模式并在文本文件中保存的日志内容 (**-f**)。

当指定一个日志文件时，UMDH 分析该文件并显示每个跟踪分配的字节数的降序顺序中的函数调用。

当你指定两个日志文件时，UMDH 比较文件，并且按降序顺序显示其分配一代代产品的两个试用版之间最多的函数调用。

<span id="_______-h____"></span><span id="_______-H____"></span> **-h | ?**  
显示帮助。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```dbgcmd
umdh dump.txt
umdh -d -v dump.txt
umdh dump1.txt dump2.txt
```

<a name="remarks"></a>备注
-------

假设您有两台计算机：*记录计算机*创建 UMDH 日志以及一个*分析计算机*分析 UMDH 日志的位置。 分析计算机上的符号路径必须指向日志时间在加载日志记录计算机的 Windows 版本的符号。 未指向符号路径分析计算机上的符号服务器。 如果这样做，UMDH 将检索分析计算机运行的 Windows 版本的符号和 UMDH 将不会显示有意义的结果。

 

 





