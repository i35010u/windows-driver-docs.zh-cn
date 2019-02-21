---
title: 调试 OCA 小型转储文件
description: 联机崩溃分析 (OCA) 是适用于 Windows 错误报告 (WER) 信息的报告机构。 贵公司可以使用 OCA 崩溃转储来分析客户问题。
ms.assetid: 56F4202D-6A5F-4177-BBFD-70DA717FF24A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2a29ec8c61a0a2e3d4873370c800ab6a80f359a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543495"
---
# <a name="debugging-oca-minidump-files"></a>调试 OCA 小型转储文件


在线崩溃分析 (OCA) 是报表的工具，以便[Windows 错误报告 (WER)](https://msdn.microsoft.com/library/windows/hardware/gg487440)信息。 贵公司可以使用 OCA 崩溃转储来分析客户问题。

## <a name="span-idanalyzedumpfilesspanspan-idanalyzedumpfilesspanspan-idanalyzedumpfilesspananalyze-dump-files"></a><span id="Analyze_dump_files"></span><span id="analyze_dump_files"></span><span id="ANALYZE_DUMP_FILES"></span>分析转储文件


转储文件是发生崩溃时计算机（或进程）状态的快照。

若要分析此数据，开发人员必须使用可以读取用户小型转储文件的调试程序。 调试程序还必须能够同时访问与转储文件内容匹配的映像和符号。 大多数开发人员已经注意到需要调试实时故障时使用匹配的符号。 但是，在调试小型转储，匹配映像还必须可用于调试程序。

由于小型转储文件存储的信息非常少，而且它们只存储发生崩溃时的一些不稳定信息，因此匹配的映像必须处于可用状态。 它们不存储计算机加载到内存的基本代码流。 为了节省空间，小型转储文件仅存储在发生崩溃的计算机上加载的映像的名称和时间戳。

若要检查在发生崩溃的计算机上运行的代码，调试程序必须能够访问发生崩溃的计算机上运行的相同二进制文件。 当开发人员需要调试崩溃时，调试程序使用存储在小型转储文件中的名称和时间戳对二进制文件进行独特地匹配和加载。

在调试程序中加载了映像和符号后，你可以分析发生崩溃时系统的状态，其中包括崩溃发生后保存的数据。 然而，小型转储无法重现导致特定故障的步骤。 要查找根本原因，需要分析驱动程序的源代码，以确定可能会导致故障的代码路径。 经验表明，分析转储文件和源代码可以了解和处理大多数故障。

## <a name="span-idusesymbolstomatchexecutablecodewithsourcecodespanspan-idusesymbolstomatchexecutablecodewithsourcecodespanspan-idusesymbolstomatchexecutablecodewithsourcecodespanuse-symbols-to-match-executable-code-with-source-code"></a><span id="Use_symbols_to_match_executable_code_with_source_code"></span><span id="use_symbols_to_match_executable_code_with_source_code"></span><span id="USE_SYMBOLS_TO_MATCH_EXECUTABLE_CODE_WITH_SOURCE_CODE"></span>使用符号来匹配包含源代码的可执行代码


访问匹配的映像和符号的最佳方式是使用 Microsoft 符号服务器。 符号是使调试程序能够将可执行代码映射回源代码的数据。 构建程序时，通常将程序的符号存储在符号文件中。 当调试程序分析某个程序时，它需要访问程序的符号。

符号文件可以包含以下任意或全部内容：

-   所有函数的名称和地址。
-   所有数据类型、结构和类定义。
-   全局变量的名称、数据类型和地址。
-   局部变量的名称、数据类型、地址和范围。
-   对应于每个二进制指令的源代码中的行号。

[Windows 驱动程序工具包 (WDK)](https://msdn.microsoft.com/library/windows/hardware/gg487463) 包括一些可用于减少符号文件中符号数量的工具。 将包含所有源级信息的符号文件称为完整的符号文件。 简化信息的符号文件被称为剥离符号文件。

由于符号数据对于从 Windows 错误报告 (WER) 数据中获取有意义的崩溃信息至关重要，因此鼓励你在提交要签名的驱动程序时提交符号。 提交符号时，将它们存储在服务器上，从而使符号数据与相关联的 WER 进程同步。 通过此存储流程，你可以轻松地对小型转储文件中报告的崩溃进行分类，并最终接收从 Microsoft 返回的更佳数据。

Microsoft 在 Internet 上提供符号服务器，你可以使用它来分析显示在小型转储文件中的 Windows 模块。 此服务器包括 Windows 中的剥离符号文件和其他一些产品。 Microsoft Windows XP 和 Windows Server 2003 添加了二进制文件。 可以使用 Internet 符号服务器和 Windows 调试工具来分析小型转储文件。

## <a name="span-idintegratewerintoapplicationsspanspan-idintegratewerintoapplicationsspanspan-idintegratewerintoapplicationsspanintegrate-wer-into-applications"></a><span id="Integrate_WER_into_applications"></span><span id="integrate_wer_into_applications"></span><span id="INTEGRATE_WER_INTO_APPLICATIONS"></span>将 WER 集成到应用程序


有关将 WER 集成到应用程序中的更多信息，请参阅[使用 WER](https://msdn.microsoft.com/library/bb513616.aspx)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[高级驱动程序调试\[336 KB\] \[PPT\]](https://download.microsoft.com/download/f/0/5/f05a42ce-575b-4c60-82d6-208d3754b2d6/adv-drv_debug.ppt)

[WDK 和 WinDbg 下载](https://go.microsoft.com/fwlink/p/?LinkId=733614)

[驱动程序调试基础知识\[WinHEC 2007; 633 KB\] \[PPT\]](https://download.microsoft.com/download/a/f/d/afdfd50d-6eb9-425e-84e1-b4085a80e34e/dvr-t410_wh07.pptx)

[如何读取 Windows 如果发生了崩溃，创建很小的内存转储文件](https://support.microsoft.com/kb/315263)

[资源定义语句](https://msdn.microsoft.com/library/aa381043.aspx)

[Windows 错误报告](https://msdn.microsoft.com/library/bb513641(vs.85).aspx)

[VERSIONINFO 资源](https://msdn.microsoft.com/library/aa381058.aspx)

 

 






