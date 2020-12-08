---
title: 分析 UMDH 日志
description: 使用以下命令分析通过使用分析正在运行的进程中所述语法运行 UMDH 创建的 User-Mode 转储堆 (UMDH) 日志。
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
ms.openlocfilehash: aa3157d4a0840a0d3b7e3e028f9da9f7be9991c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783561"
---
# <a name="analyze-umdh-logs"></a>分析 UMDH 日志


使用以下命令分析通过使用 [**分析正在运行的进程**](analyze-a-running-process.md)中所述语法运行 UMDH 创建的 User-Mode 转储堆 (UMDH) 日志。 此分析侧重于分配，而不是堆栈跟踪。

你可以分析单个日志文件或比较不同运行的日志，以检测程序或驱动程序在一段时间内的内存转储分配中的更改。

```dbgcmd
umdh [-d] [-v] [-l] File1 [File2] [-h | ?]
```

## <a name="span-idddk_analyze_umdh_logs_dtoolsspanspan-idddk_analyze_umdh_logs_dtoolsspanparameters"></a><span id="ddk_analyze_umdh_logs_dtools"></span><span id="DDK_ANALYZE_UMDH_LOGS_DTOOLS"></span>参数


<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
以十进制数字显示数值数据。 默认值为十六进制。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
详细模式。 包括跟踪和摘要信息。 分析单个日志文件时，这些跟踪非常有用。

<span id="_______-l______"></span><span id="_______-L______"></span>**-l**   
在日志中包括文件名和行号。  (请注意，参数是 lowercased 字母 "L" 而不是数字一。 ) 

<span id="_______File1__File2_"></span><span id="_______file1__file2_"></span><span id="_______FILE1__FILE2_"></span>*File1* \[*File2*\]  
指定要分析的 UMDH 日志文件。

当你在 " [**分析正在运行的进程**](analyze-a-running-process.md) " 模式下运行日志文件并将日志内容保存到 (**-f**) 的文本文件中时，UMDH 将创建日志文件。

指定一个日志文件时，UMDH 将分析文件，并按分配的字节数降序显示每个跟踪中的函数调用。

当你指定两个日志文件时，UMDH 将对文件进行比较，并按降序顺序显示其分配在两次试验之间增长最多的函数调用。

<span id="_______-h____"></span><span id="_______-H____"></span>**-h |？**  
显示帮助。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```dbgcmd
umdh dump.txt
umdh -d -v dump.txt
umdh dump1.txt dump2.txt
```

<a name="remarks"></a>备注
-------

假设您有两台计算机：一 *台日志记录计算机* ，您可以在其中创建 UMDH 日志以及分析 UMDH 日志的 *分析计算机* 。 分析计算机上的符号路径必须指向在日志记录时日志记录计算机上加载的 Windows 版本的符号。 不要将分析计算机上的符号路径指向符号服务器。 如果这样做，UMDH 将检索分析计算机上运行的 Windows 版本的符号，UMDH 将不会显示有意义的结果。

 

 





