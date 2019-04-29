---
title: 如何在静态库中使用 WPP
description: 如何在静态库中使用 WPP
ms.assetid: 02e13837-f8c7-4824-a4db-5e8b49fdcb59
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24dbd13c108e0e9e16c139354eab9dd5be8985e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390534"
---
# <a name="how-do-i-use-wpp-in-static-libraries"></a>如何在静态库中使用 WPP？


可以使用 WPP 跟踪内的静态库中提供了对之间的静态库 (.lib) 和二进制文件 （.exe、.dll 或.sys） 跟踪的单独控制的方式使用它。

二进制文件和库具有其自己的控件的 GUID。 这允许在静态库、 二进制文件，或两者中启用的跟踪。

可以通过几个点上使用 WPP 访问.lib 文件，如下面的代码示例中所示。 请注意，务必不定义实际值的控件的 GUID，因为静态库不调用 WPP\_INIT\_跟踪宏，它会使用 ETW 的实际注册。

```
#define WPP_CONTROL_GUIDS \
WPP_DEFINE_CONTROL_GUID(mylib,(0,0,0,0,0), \
WPP_DEFINE_BIT(Error) \
WPP_DEFINE_BIT(Unusual) \
WPP_DEFINE_BIT(Noise) \
)
```

使用库的.dll、.exe 和.sys 文件必须调用 WPP\_INIT\_跟踪，这将向 WPP 注册提供程序。 二进制文件的调用宏 WPP\_INIT\_跟踪必须有一份 WPP 控件通过 WPP 获取的 Guid\_控制\_GUID 宏。 仅当计划在静态库中定义的标志还使用该二进制文件中，所需的标志值的副本。

在下面的代码示例中，首先声明静态库控件 GUID 和控制 GUID 标志匹配在库中定义的标志：

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

您可以选择所需跟踪在你的组件和静态库，只需指定两个单独的控件 GUID.lib 文件和.exe 文件中，每个都有它自己的标志或一个控件 GUID 的控制度。 在示例中，该.exe 文件正在使用相同的标记作为.lib 文件。

 

 





