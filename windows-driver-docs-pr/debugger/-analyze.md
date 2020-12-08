---
title: analyze
description: "\"分析\" 扩展显示有关当前异常或 bug 检查的信息。"
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
ms.openlocfilehash: 2aa15cd486cc2063c0d907d0011d328910c59b03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800049"
---
# <a name="analyze"></a>!analyze


**！分析** 扩展显示有关当前异常或 bug 检查的信息。

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

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示详细输出。

<span id="-f"></span><span id="-F"></span>**-f**  
生成 **！分析** 异常输出。 使用此参数可查看异常分析，即使调试器未检测到异常时也是如此。

<span id="-hang"></span><span id="-HANG"></span>**-挂起**  
生成 **！分析** 挂起应用程序的输出。 如果目标遇到 bug 检查或异常，则使用此参数，但对应用程序挂起的原因的分析与问题更相关。 在内核模式下， **！分析** **-挂起** 调查系统持有的锁，然后扫描 DPC 队列链。 在用户模式下， **！分析** **-挂起** 会分析线程堆栈，以确定是否有任何线程正在阻止其他线程。

在用户模式下运行此扩展之前，请考虑将当前线程更改为你认为已停止响应的线程 (即挂起) ，因为异常可能已将当前线程更改为其他线程。

<span id="_______-D_______BucketID______"></span><span id="_______-d_______bucketid______"></span><span id="_______-D_______BUCKETID______"></span>**-D** *BucketID*   
仅显示与指定 *BucketID* 相关的那些项。

<span id="_______-show_______BugCheckCode___BugParameters_"></span><span id="_______-show_______bugcheckcode___bugparameters_"></span><span id="_______-SHOW_______BUGCHECKCODE___BUGPARAMETERS_"></span>**-show** *BugCheckCode* \[ *BugParameters*\]  
显示 *BugCheckCode* 指定的 bug 检查的相关信息。 *BugParameters* 指定最多四个 bug 检查参数（用空格分隔）。 您可以使用这些参数进一步优化搜索。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
调试器遇到已知问题时继续执行。 如果此问题不是 "已知" 问题，调试器将在目标中保持不变。

你可以将 **-c** 选项与以下子参数一起使用。 这些子参数配置已知问题的列表。 它们不会导致自身执行。 在运行 **！至少分析** **-c**  ****  **-load** 一次后， **！分析** **-c** 不起作用。

<span id="-load_KnownIssuesFile"></span><span id="-load_knownissuesfile"></span><span id="-LOAD_KNOWNISSUESFILE"></span>**-load** *KnownIssuesFile*  
加载指定的已知问题文件。 *KnownIssuesFile* 指定该文件的路径和文件名。 此文件必须为 XML 格式。 您可以在 sdk 示例中找到示例文件，以便 \\ \\ 分析 \_ 调试器安装目录的继续子目录。  (必须已执行完 Windows 调试工具的完全安装才能使用此文件。 ) 

KnownIssuesFile 文件中的已知问题的列表用于所有 *KnownIssuesFile* 的 **c** 命令，直到你使用 **-c**  ****  **-卸载** 为止，或直到再次使用 **-c**  ****  **加载** 之后 (新数据将替换旧数据) 。

<span id="-unload"></span><span id="-UNLOAD"></span>**-unload**  
卸载当前的已知问题列表。

<span id="-help"></span><span id="-HELP"></span>**-help**  
显示调试器中的 **！分析** **-c** 扩展命令扩展的帮助 [命令窗口](debugger-command-window.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ext.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关用户模式异常和内核模式停止错误的示例分析 (即，崩溃) ，以及有关如何 **！分析** 如何使用 triage.ini 文件的详细信息，请参阅 [使用！分析扩展](using-the--analyze-extension.md)。

<a name="remarks"></a>备注
-------

在用户模式下， **！分析** 显示有关当前异常的信息。

在内核模式下， **！分析** 显示有关最新 bug 检查的信息。 如果发生错误检查，则会自动生成 " **！分析** " 显示。 可以使用 **！分析** **-v** 来显示其他信息。 如果只想查看基本 bug 检查参数，可以使用 [**错误检查 (显示 Bug 检查数据)**](-bugcheck--display-bug-check-data-.md) 命令。

对于使用 User-Mode Driver Framework (UMDF) 版本2.15 或更高版本的驱动程序， **！分析** 提供有关 UMDF 验证程序失败和未经处理的异常的信息。 此功能在执行实时内核模式调试时可用，同时也可用于分析用户模式内存转储文件。 对于 UMDF 驱动程序崩溃， **！分析** 尝试识别负责的驱动程序。

 

 





