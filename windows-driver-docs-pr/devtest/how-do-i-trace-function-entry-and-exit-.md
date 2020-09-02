---
title: 如何实现 trace 函数进入和退出
description: 如何实现 trace 函数进入和退出
ms.assetid: 08b0cf86-0f19-4972-8ae1-44ffdc968c16
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f13de0ae90edbd6ed687a6a126701eaa9c60b6ec
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383173"
---
# <a name="how-do-i-trace-function-entry-and-exit"></a>如何跟踪函数入口和出口？


下面的示例代码演示如何跟踪函数进入和退出调用。 此代码适用于 Windows 2000 和更高版本的 Windows。

首先，将 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的定义添加到源文件或头文件。 定义 [跟踪标志](trace-flags.md)时，为函数跟踪定义一个标志，如以下示例中所示：

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(ERROR)                \
        WPP_DEFINE_BIT(Unusual)              \
        WPP_DEFINE_BIT(Noise)                \
 WPP_DEFINE_BIT(FuncTrace) )
```

然后，在同一文件中，添加跟踪消息的配置数据。 使用 **begin \_ wpp config** 语句启动配置数据，并以 **结束 \_ wpp** 语句结束。 然后，添加支持 FuncTrace 的宏的定义。

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

在源文件中，将函数代码与 FuncEntry 括起来 ** ( # B1 ** 和 **FuncExit ( # B3 ** 调用。

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

如果将配置数据放在标头文件中，请使用 **-scan** 参数指示 WPP 查找指定文件中的配置数据。 在此示例中，配置数据位于 mytrace 文件中。

```
RUN_WPP=$(SOURCES) -km -scan:mytrace.h
```

**注意**  不能在用户模式应用程序或动态链接库的 "运行 WPP" 指令中指定 **-公里** 开关 \_ (dll) 。



有关运行 WPP 的可选参数的完整列表 \_ ，请参阅 [WPP 预处理器](wpp-preprocessor.md)。