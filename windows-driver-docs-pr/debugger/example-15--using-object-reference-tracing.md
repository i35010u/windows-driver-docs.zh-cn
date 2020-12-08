---
title: 示例15使用对象引用跟踪
description: 示例15使用对象引用跟踪
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 108bdd0e927ec04863b8e7ef738bde73292135d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838525"
---
# <a name="example-15-using-object-reference-tracing"></a>示例 15：使用对象引用跟踪


对象引用跟踪是一项 Windows 功能，它在引用或取消引用对象时记录顺序堆栈跟踪。 它旨在检测可能导致崩溃或内存泄漏的对象处理错误。 其中一些错误很难检测，因为它们不是一致地显示。 有关详细信息，请参阅 [对象引用跟踪](object-reference-tracing.md)。

您可以通过使用 " **全局标志** " 对话框或在命令提示符处配置对象引用跟踪。 下面的示例使用命令提示符。 有关使用 " **全局标志** " 对话框配置对象引用跟踪的信息，请参阅 [配置对象引用跟踪](configuring-object-reference-tracing.md)。

您可以使用 Gflags 来启用、禁用和配置对象引用跟踪。 流程如下：

-   **使用 Gflags 可以在注册表中启用对象引用跟踪** ，或在运行时) 设置 (运行时使用内核标志。 如果将此设置添加到注册表，则必须重新启动计算机才能启动跟踪。 如果启用设置的运行时版本，则跟踪会立即开始，但当你关闭或重新启动计算机时，跟踪设置将恢复为注册表项中的设置。

-   **启动创建可疑对象的过程**。 跟踪仅包括在跟踪开始后启动的进程创建的对象。 如果在重新启动过程中或一段时间后启动进程，请将跟踪设置添加到注册表，然后重新启动系统。

-   **使用** [**！ obtrace**](-obtrace.md) **调试器扩展** 来查看跟踪。 默认情况下，将一直维护跟踪直到对象被销毁，但你可以使用 **/p** 参数维护跟踪，直到禁用跟踪。

-   **使用 Gflags 禁用对象引用跟踪**。在注册表中，或作为内核标志 (运行时) 设置。 如果从注册表删除设置，则必须重新启动计算机以结束跟踪。 如果禁用设置的运行时版本，则跟踪会立即结束，但当你关闭或重新启动计算机时，跟踪设置将恢复为注册表中的设置。

这些示例演示如何使用 Gflags 来启用和禁用对象引用跟踪。 \\

### <a name="span-idenable_run_time_tracingspanspan-idenable_run_time_tracingspanenable-run-time-tracing"></a><span id="enable_run_time_tracing"></span><span id="ENABLE_RUN_TIME_TRACING"></span>启用运行时跟踪

以下命令在命令提示符下启用对象引用跟踪。 该命令使用 **/ko** 参数启用对象引用跟踪作为内核标志 (运行时) 设置。 该命令使用 **/t** 参数指定池标记 **Tag1** 和 **Fred**。 因此，将跟踪使用 **Tag1** 或 **Fred** 创建的所有对象。

```console
gflags /ko /t Tag1;Fred
```

由于该命令会将内核标志更改 (运行时) 设置，因此将立即开始对象引用跟踪。 此跟踪将包含所有对象，这些对象具有在提交命令后启动的进程创建的池标记 **Tag1** 或 **Fred** 。

Gflags 通过打印以下消息进行响应：

```console
Running Kernel Settings :
Object Ref Tracing Enabled
        Temporary Traces
        Pool Tags: Tag1;Fred
        Process Name: All Processes
```

此消息表示启用了对象引用跟踪。 "临时跟踪" 表示在销毁对象时删除跟踪的所有记录。 若要使跟踪 "永久化"，请使用 **/p** 参数，该参数指示 Windows 保留跟踪数据，直到禁用对象引用跟踪或关闭或重新启动计算机。

### <a name="span-idenable_tracing_in_the_registryspanspan-idenable_tracing_in_the_registryspanenable-tracing-in-the-registry"></a><span id="enable_tracing_in_the_registry"></span><span id="ENABLE_TRACING_IN_THE_REGISTRY"></span>在注册表中启用跟踪

以下命令将对象引用跟踪配置添加到注册表。 重新启动计算机时，将开始配置的跟踪。

该命令使用 **/ro** 参数启用对象引用跟踪作为注册表设置。 该命令使用 **/i** 指定 notepad.exe 的进程，并使用 **/T** 参数指定 **Tag1** 和 **Fred** 的池标记。 因此，使用 **Tag1** 或 **Fred** 池标记创建的所有对象都将被跟踪。 该命令还使用 **/p** 参数，该参数将保留跟踪数据，直到禁用跟踪。

```console
gflags /ro /t Tag1;Fred /i Notepad.exe /p
```

提交该命令时，Gflags 会将信息存储在注册表中。 但是，因为在您重新启动计算机之前，注册表设置是无效的，所以此对象引用跟踪已配置，但尚未启动。

Gflags 通过打印以下消息进行响应：

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

此消息表示在注册表中启用了对象引用跟踪。 "永久跟踪" 表示在关闭或重新启动计算机之前将保留跟踪数据。 该消息还会列出要跟踪的池标记和映像文件的名称。

### <a name="span-iddisplay_the_object_reference_tracing_configurationspanspan-iddisplay_the_object_reference_tracing_configurationspandisplay-the-object-reference-tracing-configuration"></a><span id="display_the_object_reference_tracing_configuration"></span><span id="DISPLAY_THE_OBJECT_REFERENCE_TRACING_CONFIGURATION"></span>显示对象引用跟踪配置

可以显示当前有效的对象引用跟踪配置，或将其存储在计算机重新启动时要使用的注册表中。

在此示例中，有一个对象引用跟踪配置存储在注册表中，另一个对象引用配置为运行时。 运行时跟踪会立即开始 (并覆盖) 的任何注册表设置。 但是，如果重新启动系统，则运行时设置将丢失，并且对象引用跟踪会话注册表设置将生效。

以下命令显示运行时对象引用跟踪配置。 它使用不带任何其他参数的 **/ko** 参数。

```console
gflags /ko
```

```console
Running Kernel Settings :
Object Ref Tracing Enabled
        Temporary Traces
        Pool Tags: Tag1;Fred
        Process Name: All Processes
```

如果启用对象引用跟踪（如本示例所示），则显示的设置将描述正在进行的跟踪。

以下命令显示注册表中存储的对象引用跟踪配置数据。 它使用不带任何其他参数的 **/ro** 参数。

```console
gflags /ro
```

作为响应，Gflags 显示注册表中存储的数据：

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

如果已重新启动计算机，因为你已将对象引用跟踪配置添加到注册表，则响应 gflags/ro 命令时显示的设置将描述正在进行的跟踪。 但是，如果尚未重新启动，或者重新启动了运行时对象引用跟踪 (**/ko**) ，则注册表中存储的设置当前不起作用，但当你重新启动系统时，它们将再次生效。

### <a name="span-iddisable_object_reference_tracingspanspan-iddisable_object_reference_tracingspandisable-object-reference-tracing"></a><span id="disable_object_reference_tracing"></span><span id="DISABLE_OBJECT_REFERENCE_TRACING"></span>禁用对象引用跟踪

禁用 (内核标志) 对象引用跟踪设置时，跟踪会立即停止。 如果在注册表中禁用对象引用跟踪设置，则重新启动计算机时跟踪将停止。

以下命令将禁用运行时对象引用跟踪。 它使用 **/d** 参数禁用所有设置。 不能有选择地禁用设置。

```console
gflags /ko -d
```

命令成功后，Gflags 将会出现以下消息：

```console
Running Kernel Settings :
Object Ref Tracing Disabled
```

以下命令将禁用运行时对象引用跟踪。

以下命令禁用注册表中的对象引用跟踪设置。 它使用 **/d** 参数禁用所有设置。 不能有选择地禁用设置。 当你重新启动计算机时，此命令有效。

```console
gflags /ro -d
```

命令成功后，Gflags 将会出现以下消息：

```console
Boot Registry Settings :
Object Ref Tracing Disabled
```

 

 





