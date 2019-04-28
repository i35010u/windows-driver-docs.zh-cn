---
title: 分析
description: 分析扩展显示有关当前异常或错误检查的信息。
ms.assetid: dec760fb-0af6-4504-9855-8fe63c1c9783
keywords:
- 分析 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- analyze
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73f26868420f3cd2a08328fae9117ffaf824d70e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334754"
---
# <a name="analyze"></a>!analyze


**！ 分析**扩展显示有关当前异常或错误检查的信息。

User-Mode

```dbgcmd
    !analyze [-v] [-f | -hang] [-D BucketID] 
    !analyze -c [-load KnownIssuesFile | -unload | -help ]
```

Kernel-Mode

```dbgcmd    
    !analyze [-v] [-f | -hang] [-D BucketID] 
    !analyze -c [-load KnownIssuesFile | -unload | -help ]
    !analyze -show BugCheckCode [BugParameters]
```

## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示详细输出。

<span id="-f"></span><span id="-F"></span>**-f**  
将生成 **！ 分析**异常输出。 使用此参数以查看异常分析，即使在调试器不会检测异常。

<span id="-hang"></span><span id="-HANG"></span>**-hang**  
将生成 **！ 分析**挂起应用程序输出。 当目标遇到的错误检查或异常，但应用程序挂起原因的分析更贴近您的问题时，请使用此参数。 在内核模式下 **！ 分析** **-挂起**调查系统保存，然后再进行扫描的 DPC 队列链的锁。 在用户模式下 **！ 分析** **-挂起**分析以确定是否任何线程来阻止其他线程的线程堆栈。

在用户模式下运行此扩展之前，请考虑更改为您认为已停止响应 （挂起） 的因为异常可能已更改当前线程，到另一个线程的当前线程。

<span id="_______-D_______BucketID______"></span><span id="_______-d_______bucketid______"></span><span id="_______-D_______BUCKETID______"></span> **-D** *BucketID*   
显示与指定项*BucketID*。

<span id="_______-show_______BugCheckCode___BugParameters_"></span><span id="_______-show_______bugcheckcode___bugparameters_"></span><span id="_______-SHOW_______BUGCHECKCODE___BUGPARAMETERS_"></span> **-show** *BugCheckCode* \[*BugParameters*\]  
显示有关指定的错误检查的信息*BugCheckCode*。 *BugParameters*最多指定四个 bug 检查参数以空格分隔。 这些参数，你可以进一步优化搜索。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
当调试器遇到的已知的问题，请继续执行。 如果此问题不是"已知"问题，该调试器将保持分解为目标。

可以使用 **-c**具有以下子参数选项。 这些子参数配置已知问题的列表。 它们不会导致进行单独执行。 直到你运行 **！ 分析** **-c** **** **-加载**至少一次 **！ 分析** **-c**没有任何影响。

<span id="-load_KnownIssuesFile"></span><span id="-load_knownissuesfile"></span><span id="-LOAD_KNOWNISSUESFILE"></span>**-加载** *KnownIssuesFile*  
加载指定的已知问题的文件。 *KnownIssuesFile*指定此文件的路径和文件。 此文件必须采用 XML 格式。 可以在 sdk 中找到示例文件\\示例\\分析\_继续调试程序安装目录的子目录。 （你必须执行调试工具的 Windows 以将此文件的完整的安装。）

中的已知问题列表*KnownIssuesFile*文件用于所有更高版本 **-c**直到您使用的命令 **-c** **** **-卸载**，或直到您使用 **-c** **** **-加载**再次 （此时新的数据替换旧的数据）。

<span id="-unload"></span><span id="-UNLOAD"></span>**-unload**  
卸载当前的已知问题列表。

<span id="-help"></span><span id="-HELP"></span>**-help**  
显示的帮助 **！ 分析** **-c**扩展命令中的扩展[调试器命令窗口](debugger-command-window.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

示例分析和内核模式的用户模式异常停止错误 （即，崩溃），并详细了解如何 **！ 分析**使用 triage.ini 文件，请参阅[Using ！ 分析扩展](using-the--analyze-extension.md)。

<a name="remarks"></a>备注
-------

在用户模式下 **！ 分析**显示有关当前异常的信息。

在内核模式下 **！ 分析**显示最新的 bug 检查有关的信息。 出现的 bug 检查时， **！ 分析**显示自动生成。 可以使用 **！ 分析** **-v**以显示其他信息。 如果想要查看仅基本 bug 检查参数，则可以使用[ **.bugcheck （显示 Bug 检查数据）** ](-bugcheck--display-bug-check-data-.md)命令。

使用用户模式驱动程序框架 (UMDF) 2.15 或更高版本，版本的驱动程序 **！ 分析**提供 UMDF 验证程序失败和未经处理的异常有关的信息。 当执行实时内核模式调试，以及分析用户模式内存转储文件时，此功能才可用。 UMDF 驱动程序损坏 **！ 分析**尝试识别负责驱动程序。

 

 





