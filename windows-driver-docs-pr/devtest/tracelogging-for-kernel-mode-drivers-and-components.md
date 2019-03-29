---
title: 内核模式驱动程序和组件的 TraceLogging
description: 本主题介绍如何使用 TraceLogging API 从内核模式驱动程序和组件中。
ms.assetid: 6AF8DD2C-400F-4E9D-A6DF-40A847BCBD76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b98d079b1c206957e4d92db710f24c0d8dffad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567506"
---
# <a name="tracelogging-for-kernel-mode-drivers-and-components"></a>内核模式驱动程序和组件的 TraceLogging

本主题介绍如何使用[TraceLogging](https://docs.microsoft.com/windows/desktop/tracelogging/trace-logging-portal)从内核模式驱动程序和组件中的 API。

先决条件：

- Windows 10
- Visual Studio 2013 （或更高版本）
- Windows 10 SDK
- 适用于 Windows 10 的 Windows 驱动程序工具包 (WDK)

## <a name="include-the-tracelogging-header-files"></a>包括 TraceLogging 标头文件

若要使用 TraceLogging API，包括 TraceLogging 标头文件 TraceLoggingProvider.h。 其他 TraceLogging API 标头文件，TraceLoggingActivity.h，才可供 c + + 编写的用户模式驱动程序中使用。

```command
#include <wdm.h>
#include <TraceLoggingProvider.h> 
```

> [!NOTE]
> 开发内核模式驱动程序时需要为 TraceLoggingProvider.h wdm.h 中的文件。

## <a name="declare-your-driver-as-a-tracelogging-provider"></a>将您的驱动程序声明为 TraceLogging 提供程序

1. 添加[ **TRACELOGGING\_DECLARE\_提供程序**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider)宏声明提供程序的句柄变量。 该宏的语法：

    ```command
    TRACELOGGING_DECLARE_PROVIDER(hProviderVariableName)
    ```

    下面的示例 TraceLogging 语句声明名为的变量*g\_hProvider*。

    ```command
    TRACELOGGING_DECLARE_PROVIDER(g_hProvider);
    ```

    使用声明的变量[ **TRACELOGGING\_DECLARE\_提供程序**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider)调用时将成为该提供程序的句柄[ **TRACELOGGING\_定义\_提供程序**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)在代码中更高版本的宏。

    > [!NOTE]
    > 你可能想要将此宏放在头文件，这样的句柄 TraceLogging 提供程序在全球提供。

2. 添加[ **TRACELOGGING\_定义\_提供程序**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)宏，并指定跟踪提供程序和跟踪提供程序句柄的名称。 该句柄已在步骤 1 中声明的变量。 该宏的语法是：

    ```command
    TRACELOGGING_DEFINE_PROVIDER(hProviderVariableName, "ProviderName", providerId [,option])
    ```

    例如，下面的语句定义名为 MyTraceLoggingProviderKM 的提供程序并将其分配给句柄 g\_hProvider。 ProviderId 参数是 ETW 提供程序 GUID。

    ```command
    TRACELOGGING_DEFINE_PROVIDER(g_hProvider, "MyTraceLoggingProviderKM",
        (0xb3864c38, 0x4273, 0x58c5, 0x54, 0x5b, 0x8b, 0x36, 0x08, 0x34, 0x34, 0x71));
    ```

    [ **TRACELOGGING\_定义\_提供程序**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)宏分配存储提供程序，并定义为提供程序的全局句柄的相应变量。 提供程序名称必须是字符串文本 （而不是变量），并且不得包含任何\\0' 字符。 只要原始句柄处于范围内，句柄和句柄的副本都有效。

    当你首次创建使用句柄**TRACELOGGING\_定义\_提供程序**宏，该提供程序是在未注册状态。 在此状态下，该提供程序将忽略，任何跟踪写入调用直至其注册。

    > [!NOTE]
    > 适用于内核模式，请注意，当提供程序元数据显式存储到 TLG\_元数据\_段 (.rdata) 为句柄创建的变量 (例如，g\_hProvider) 和 （适用于提供程序的名称示例中，"MyTraceLoggingProviderKM"） 不显式分配一个段，并将使用当前的隐式段。

**TRACELOGGING\_定义\_提供程序**宏需要传递给它处于非分页缓冲池的变量。 如果这不是这种情况已，调用方必须设置通过数据段\#杂注数据\_seg （适用于 uniqueVarName) 或通过 const 段\#杂注 const\_seg (为 g\_hMyProvider) 之前调用**TRACELOGGING\_定义\_提供程序**宏。

## <a name="register-the-driver-with-tracelogging"></a>注册 TraceLogging 驱动程序

在你**DriverEntry**函数，必须注册 TraceLogging 提供程序。
若要向 TraceLogging 注册提供程序，请将添加到 TraceLoggingRegister 宏**DriverEntry**:

```command
// Register the TraceLogging provider in the DriverEntry method.
TraceLoggingRegister(g_hProvider);
```

## <a name="unregister-the-provider-in-the-driver-unload-or-cleanup-routine"></a>取消注册中的驱动程序卸载或清理例程的提供程序

在你**DriverUnload**或清理函数中，取消注册 TraceLogging 提供程序。

```command
// Stop TraceLogging and unregister the provider
TraceLoggingUnregister(g_hProvider);
```

## <a name="log-events-in-your-code"></a>在代码中的日志事件

TraceLogging 提供日志记录事件的宏。

基本宏[ **TraceLoggingWrite**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingwrite)。 此宏的语法如下：

```command
TraceLoggingWrite(g_hProvider, "EventName", args...)
```

其中 g\_hProvider 是您定义的提供程序的句柄和"EventName"是一个字符串，用于标识特定事件的文本 （而不是变量）。 像**printf**或**DbgPrint**，则**TraceLoggingWrite**宏支持个数可变的 （最多 99) 的其他参数。 参数 （参数） 必须是 TraceLogging 包装宏，如[ **TraceLoggingLevel**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogginglevel)， [TraceLoggingInt32](https://docs.microsoft.com/windows/desktop/tracelogging/tracelogging-wrapper-macros)，或[TraceLoggingString](https://docs.microsoft.com/windows/desktop/tracelogging/tracelogging-wrapper-macros). TraceLogging 包装宏 TraceLoggingProvider.h 中定义。

> [!NOTE]
> 如果使用的 c + +，则可以使用[ **TraceLoggingValue** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingvalue)包装宏以进行自动调整的类型。 如果用 C 编写您的驱动程序，则必须使用特定于类型的字段宏 (例如， **TraceLoggingInt32**或**TraceLoggingUnicodeString**)。

下面的示例提供程序，记录一个事件 g\_hProvider。 此事件时调用"MyDriverEntryEvent。" 该宏利用 TraceLoggingPointer 和 TraceLoggingUnicodeString 包装器将写入跟踪日志的驱动程序对象和注册表路径的指针。 TraceLoggingUnicodeString 包装器采用的可选名称。 在此示例中，"RegPath"是 RegistryPath 值的名称。 如果未不指定任何名称，值用作名称。

```command
TraceLoggingWrite(
        g_hProvider,
        "MyDriverEntryEvent",
        TraceLoggingPointer(DriverObject),
        TraceLoggingUnicodeString(RegistryPath, "RegPath")); 
);
```

如果要检测内核模式驱动程序 （在 C 中)，则链接到 TraceLoggingProvider.h，可以使用**TraceLoggingWrite**， **TraceLoggingWriteActivity**，或**TraceLoggingActivityMarker**宏。 跟踪日志记录的示例，请参阅[TraceLogging 示例](tracelogging-examples.md)。

如果要检测的驱动程序或组件，它用 c + + 编写的则链接到 TraceLoggingProvider.h 和 TraceLoggingActivity.h。 当你链接到 c + + 标头时，可以记录使用事件**TraceLoggingWriteStart**， **TraceLoggingWriteStop**，并**TraceLoggingWriteTagged**宏。

有关如何捕获和查看 TraceLogging 数据的示例，请参阅[捕获和查看 TraceLogging 数据](capture-and-view-tracelogging-data.md)。
