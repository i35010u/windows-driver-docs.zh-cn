---
title: 内核模式驱动程序和组件的 TraceLogging
description: 本主题介绍如何使用内核模式驱动程序和组件中的 TraceLogging API。
ms.assetid: 6AF8DD2C-400F-4E9D-A6DF-40A847BCBD76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501d039633c0e95aacd5fc5a349b9b0d6fcec39a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384867"
---
# <a name="tracelogging-for-kernel-mode-drivers-and-components"></a>内核模式驱动程序和组件的 TraceLogging

本主题介绍如何使用内核模式驱动程序和组件中的 [TraceLogging](/windows/desktop/tracelogging/trace-logging-portal) API。

先决条件：

- Windows 10
- Visual Studio 2013 (或更高版本) 
- Windows 10 SDK
- 适用于 Windows 10 的 windows 驱动程序工具包 (WDK) 

## <a name="include-the-tracelogging-header-files"></a>包含 TraceLogging 头文件

若要使用 TraceLogging API，请包含 TraceLogging 头文件 TraceLoggingProvider。 其他 TraceLogging API 头文件 TraceLoggingActivity 只可用于以 c + + 编写的用户模式驱动程序中。

```command
#include <wdm.h>
#include <TraceLoggingProvider.h> 
```

> [!NOTE]
> 开发内核模式驱动程序时，TraceLoggingProvider 需要 wdm 文件。

## <a name="declare-your-driver-as-a-tracelogging-provider"></a>将驱动程序声明为 TraceLogging 提供程序

1. 添加 [**TRACELOGGING \_ 声明 \_ 提供程序**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider) 宏以声明提供程序句柄变量。 宏具有以下语法：

    ```command
    TRACELOGGING_DECLARE_PROVIDER(hProviderVariableName)
    ```

    下面的示例 TraceLogging 语句声明名为 *g \_ hProvider*的变量。

    ```command
    TRACELOGGING_DECLARE_PROVIDER(g_hProvider);
    ```

    当你在代码中稍后调用[**TRACELOGGING \_ 定义 \_ 提供程序**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)宏时，通过[**TRACELOGGING \_ 声明 \_ 提供**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider)程序声明的变量成为提供程序的句柄。

    > [!NOTE]
    > 你可能希望将此宏放在标头文件中，以便可以在全局范围内使用 TraceLogging 提供程序的句柄。

2. 添加 [**TRACELOGGING \_ 定义 \_ 提供程序**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider) 宏，并指定跟踪提供程序的名称和跟踪提供程序句柄。 句柄是您在步骤1中声明的变量。 宏的语法为：

    ```command
    TRACELOGGING_DEFINE_PROVIDER(hProviderVariableName, "ProviderName", providerId [,option])
    ```

    例如，下面的语句定义一个名为 MyTraceLoggingProviderKM 的提供程序，并将其分配给句柄 g \_ hProvider。 ProviderId 参数是 ETW 提供程序 GUID。

    ```command
    TRACELOGGING_DEFINE_PROVIDER(g_hProvider, "MyTraceLoggingProviderKM",
        (0xb3864c38, 0x4273, 0x58c5, 0x54, 0x5b, 0x8b, 0x36, 0x08, 0x34, 0x34, 0x71));
    ```

    [**TRACELOGGING \_ 定义 \_ 提供程序**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)宏为提供程序分配存储，并定义一个对应的变量，该变量是提供程序的全局句柄。 提供程序名称必须是字符串文字， (不是变量) 并且不得包含任何 " \\ 0" 字符。 只要原始句柄处于范围内，句柄的句柄和副本就有效。

    首次用 **TRACELOGGING \_ 定义 \_ 提供程序** 宏创建句柄时，提供程序处于未注册状态。 在此状态下，提供程序将忽略任何跟踪写入调用，直到它被注册为止。

    > [!NOTE]
    > 对于内核模式，请注意，在将提供程序元数据显式存储到 TLG \_ 元数据 \_ 段 (。 rdata) 中，为该句柄创建的变量 (例如，g \_ hProvider) 和提供程序的名称 (例如，"MyTraceLoggingProviderKM" ) 未显式分配一个段，并将使用当前的隐式段。

**TRACELOGGING \_ 定义 \_ 提供程序**宏要求传递给它的变量位于非分页池中。 如果这种情况并不是这样，则调用方必须在 \# \_ \# \_ \_ 调用 **TRACELOGGING \_ 定义 \_ 提供程序** 宏之前，通过 pragma data seg (for uniqueVarName) 或 const seg (for g hMyProvider) 设置数据段。

## <a name="register-the-driver-with-tracelogging"></a>向 TraceLogging 注册驱动程序

在 **DriverEntry** 函数中，必须注册 TraceLogging 提供程序。
若要向 TraceLogging 注册提供程序，请将 TraceLoggingRegister 宏添加到 **DriverEntry**：

```command
// Register the TraceLogging provider in the DriverEntry method.
TraceLoggingRegister(g_hProvider);
```

## <a name="unregister-the-provider-in-the-driver-unload-or-cleanup-routine"></a>在驱动程序卸载或清理例程中取消注册提供程序

在 **DriverUnload** 或清理函数中，注销 TraceLogging 提供程序。

```command
// Stop TraceLogging and unregister the provider
TraceLoggingUnregister(g_hProvider);
```

## <a name="log-events-in-your-code"></a>在代码中记录事件

TraceLogging 提供了用于记录事件的宏。

基本宏为 [**TraceLoggingWrite**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingwrite)。 此宏具有以下语法：

```command
TraceLoggingWrite(g_hProvider, "EventName", args...)
```

其中 \_ ，g hProvider 是定义的提供程序的句柄，而 "事件名称" 是一个字符串文字， (用于标识特定事件的变量) 。 与 **printf** 或 **DbgPrint**类似， **TraceLoggingWrite** 宏支持 (多达 99) 的其他参数个数。 参数 (参数) 必须是 TraceLogging 包装宏，如 [**TraceLoggingLevel**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogginglevel)、 [TraceLoggingInt32](/windows/desktop/tracelogging/tracelogging-wrapper-macros)或 [TraceLoggingString](/windows/desktop/tracelogging/tracelogging-wrapper-macros)。 TraceLogging 包装宏在 TraceLoggingProvider 中定义。

> [!NOTE]
> 如果使用的是 c + +，则可以使用 [**TraceLoggingValue**](/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingvalue) 包装宏为类型自动进行调整。 如果要在 C 中编写驱动程序，则必须使用特定于类型的字段宏 (例如， **TraceLoggingInt32** 或 **TraceLoggingUnicodeString**) 。

下面的示例记录了提供程序 hProvider 的事件 \_ 。 事件名为 "MyDriverEntryEvent"。 该宏使用 TraceLoggingPointer 和 TraceLoggingUnicodeString 包装程序将指向驱动程序对象的指针和指向跟踪日志的注册表路径。 TraceLoggingUnicodeString 包装采用一个可选名称。 在此示例中，"RegPath" 是 RegistryPath 值的名称。 如果未指定名称，则将值用作名称。

```command
TraceLoggingWrite(
        g_hProvider,
        "MyDriverEntryEvent",
        TraceLoggingPointer(DriverObject),
        TraceLoggingUnicodeString(RegistryPath, "RegPath")); 
);
```

如果检测到 C) 中 (的内核模式驱动程序，则链接到 TraceLoggingProvider，可以使用 **TraceLoggingWrite**、 **TraceLoggingWriteActivity**或 **TraceLoggingActivityMarker** 宏。 有关跟踪日志记录的示例，请参阅 [TraceLogging 示例](tracelogging-examples.md)。

如果要检测用 c + + 编写的驱动程序或组件，请链接到 TraceLoggingProvider 和 TraceLoggingActivity。 链接到 c + + 标头时，可以通过 **TraceLoggingWriteStart**、 **TraceLoggingWriteStop**和 **TraceLoggingWriteTagged** 宏记录事件。

有关如何捕获和查看 TraceLogging 数据的示例，请参阅 [捕获和查看 TraceLogging 数据](capture-and-view-tracelogging-data.md)。