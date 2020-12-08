---
title: 在静态库中使用 WPP 如何实现
description: 在静态库中使用 WPP 如何实现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c71b9f0dc6c80fefd27e0bce695537f22f1cad7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826713"
---
# <a name="how-do-i-use-wpp-in-static-libraries"></a>如何在静态库中使用 WPP？


可以通过这种方式在静态库中使用 WPP 跟踪，从而单独控制静态库 () 以及使用它的二进制 ( .exe、.dll 或 .sys) 之间的跟踪。

二进制文件和库都具有自己的控件 GUID。 这允许在静态库和/或二进制文件中启用跟踪。

可以通过在多个点使用 WPP 来访问 .lib 文件，如下面的代码示例所示。 请注意，定义控件 GUID 的实际值并不重要，因为静态库不会调用 WPP \_ INIT \_ 跟踪宏，该宏会执行 ETW 的实际注册。

```
#define WPP_CONTROL_GUIDS \
WPP_DEFINE_CONTROL_GUID(mylib,(0,0,0,0,0), \
WPP_DEFINE_BIT(Error) \
WPP_DEFINE_BIT(Unusual) \
WPP_DEFINE_BIT(Noise) \
)
```

使用库的 .dll、.exe 和 .sys 文件必须调用 WPP \_ INIT \_ 跟踪，这将使用 wpp 注册该提供程序。 调用宏 WPP INIT 跟踪的二进制 \_ 文件 \_ 必须包含 wpp 控件 guid 宏获得的 Wpp 控件 guid 的副本 \_ \_ 。 仅当静态库中定义的标志还计划用于二进制文件时，才需要标记值的副本。

在下面的代码示例中，静态库的控件 GUID 首先声明，控件 GUID 的标志与库中定义的标志匹配：

```
#define WPP_CONTROL_GUIDS \
WPP_DEFINE_CONTROL_GUID(SharedStaticLibs,(81b20feb,73a8,4b62,95bc,354477c97a6f), \
WPP_DEFINE_BIT(Error) \
WPP_DEFINE_BIT(Unusual) \
WPP_DEFINE_BIT(Noise) \
) \
WPP_DEFINE_CONTROL_GUID(AppSpecificFlags,(81b20fec,73a8,4b62,95bc,354477c97a6f), \
WPP_DEFINE_BIT(EntryExit) \
WPP_DEFINE_BIT(Initialization) \
WPP_DEFINE_BIT(MemoryAllocations) \
) 
```

您可以通过为 .lib 和 .exe 文件指定单独的控件 GUID，并为二者都指定一个控件 GUID，来选择对您的组件和静态库进行跟踪所需的控制程度。 在示例中，.exe 文件使用与 .lib 文件相同的标志。

 

 





