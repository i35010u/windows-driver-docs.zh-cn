---
title: 如何实现跟踪函数进入和退出
description: 如何实现跟踪函数进入和退出
ms.assetid: 08b0cf86-0f19-4972-8ae1-44ffdc968c16
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bbb7d307999c5eab10e7ce69906c2af20fd8a11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347705"
---
# <a name="how-do-i-trace-function-entry-and-exit"></a>如何跟踪函数入口和出口？


下面的示例代码演示如何跟踪函数进入和退出调用。 此代码适用于 Windows 2000 和更高版本的 Windows。

首先，添加的定义[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏到源文件或头文件。 定义时[跟踪标志](trace-flags.md)，定义的函数跟踪标志，如下面的示例中所示：

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(ERROR)                \
        WPP_DEFINE_BIT(Unusual)              \
        WPP_DEFINE_BIT(Noise)                \
 WPP_DEFINE_BIT(FuncTrace) )
```

然后，在同一文件中，添加跟踪消息的配置数据。 启动具有的配置数据**开始\_wpp config**语句，并结束其与**最终\_wpp**语句。 然后添加支持 FuncTrace 的宏的定义。

```
// begin_wpp config
// FUNC FuncEntry();
// FUNC FuncExit();
// USESUFFIX(FuncEntry, " Entry to %!FUNC!");
// USESUFFIX(FuncExit, " Exit from %!FUNC!");
// end_wpp

// Map the null flags used by Entry/Exit to a function called FuncTrace
#define WPP__ENABLED() WPP_LEVEL_ENABLED(FuncTrace)
#define WPP__LOGGER() WPP_LEVEL_LOGGER(FuncTrace)
```

在源代码文件中，函数使用环绕代码**FuncEntry()** 并**FuncExit()** 调用。

```
#include "mytrace.h"
#include "entryexit.tmh"
void examplesub(int x)
{
    FuncEntry();
    // function code
    FuncExit();
}
```

例如：

```
#include "mytrace.h"
#include "entryexit.tmh"
void examplesub(int x)
{
    FuncEntry();
       DoTraceMessage(Noise, "Value is %d",x);
    FuncExit();
}
```

如果标头文件中将配置数据，使用 **-扫描**参数指示 WPP 查找配置数据中指定的文件。 在此示例中，配置数据是 mytrace.h 文件中。

```
RUN_WPP=$(SOURCES) -km -scan:mytrace.h
```

**请注意**您必须指定**公里**运行中切换\_WPP 指令用于用户模式应用程序或动态链接库 (Dll)。



有关运行的可选参数的完整列表\_WPP，请参阅[WPP 预处理器](wpp-preprocessor.md)。









