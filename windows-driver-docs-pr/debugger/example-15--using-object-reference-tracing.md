---
title: 例如，如果希望使用对象引用跟踪
description: 例如，如果希望使用对象引用跟踪
ms.assetid: 3c6102e6-4dac-4d90-ab8f-162dd6d8adf9
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0730f0242c1011826bfbf037f1879b81a8db2823
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521581"
---
# <a name="example-15-using-object-reference-tracing"></a>例如，如果希望：使用对象引用跟踪


对象引用跟踪是一项 Windows 功能，用于引用或取消引用某个对象时记录顺序的堆栈跟踪。 这被为了检测可能会导致崩溃或内存泄漏的对象处理中的错误。 这些错误的一些很难检测，因为它们不一致地出现。 有关详细信息，请参阅[对象引用跟踪](object-reference-tracing.md)。

可以通过使用配置对象引用跟踪**全局标志**对话框或在命令提示符。 下面的示例使用命令提示符。 有关使用信息**全局标志**对话框可以配置对象引用跟踪，请参阅[配置对象引用跟踪](configuring-object-reference-tracing.md)。

Gflags 可用于启用、 禁用和配置对象引用跟踪。 过程如下所示：

-   **请用 Gflags 启用对象引用跟踪**注册表中或作为内核标志 （运行时间） 设置。 如果将设置添加到注册表时，必须重新启动计算机以启动跟踪。 如果启用设置的运行的时版本，跟踪将立即启动，但在关闭或重新启动计算机时，跟踪设置将还原为注册表项中。

-   **开始创建可疑对象**。 跟踪包括仅由开始跟踪之后启动的进程创建的对象。 如果进程启动期间或在重新启动后很快，到注册表中，添加跟踪设置，然后重新启动系统。

-   **使用** [ **！ obtrace** ](-obtrace.md) **调试器扩展**若要查看的跟踪。 默认情况下，跟踪之前，会保留该对象被销毁，但你可以使用 **/p**参数，以维护跟踪之前禁用跟踪。

-   **使用 Gflags 禁用对象引用跟踪**。 在注册表或作为内核标志 （运行时间） 设置。 如果从注册表中删除了设置，必须重新启动计算机以结束跟踪。 如果禁用设置的运行的时版本，跟踪立即结束，但在关闭或重新启动计算机时，跟踪设置将还原为在注册表中。

这些示例显示如何使用 Gflags 来启用和禁用对象引用跟踪。 \\

### <a name="span-idenableruntimetracingspanspan-idenableruntimetracingspanenable-run-time-tracing"></a><span id="enable_run_time_tracing"></span><span id="ENABLE_RUN_TIME_TRACING"></span>启用运行时跟踪

以下命令在命令提示符下启用对象引用跟踪。 该命令使用 **/ko**参数来启用内核 （运行时间） 的标志设置为的对象引用跟踪。 该命令使用 **/t**参数来指定池标记**标记 1**并**Fred**。 因此，所有对象的创建与**标记 1**或**Fred**跟踪的情况。

```console
gflags /ko /t Tag1;Fred
```

由于该命令更改内核标志 （运行） 设置，则对象引用跟踪将立即启动。 跟踪将包括所有对象的池标记**标记 1**或**Fred**通过该命令将提交之后启动的进程创建的。

Gflags 响应通过打印以下消息：

```console
Running Kernel Settings :
Object Ref Tracing Enabled
        Temporary Traces
        Pool Tags: Tag1;Fred
        Process Name: All Processes
```

此消息表示，启用对象引用跟踪。 "临时 Traces"指示当对象被销毁时删除的跟踪的所有记录。 若要使"永久"更改跟踪，请使用 **/p**参数，以便将 Windows 保留的跟踪数据，直到对象引用跟踪处于禁用状态，或关闭或重新启动计算机。

### <a name="span-idenabletracingintheregistryspanspan-idenabletracingintheregistryspanenable-tracing-in-the-registry"></a><span id="enable_tracing_in_the_registry"></span><span id="ENABLE_TRACING_IN_THE_REGISTRY"></span>在注册表中启用跟踪

以下命令将对象引用跟踪的配置添加到注册表。 你配置的跟踪开始时重新启动计算机。

该命令使用 **/ro**参数，以便能够作为注册表设置的对象引用跟踪。 该命令使用 **/i**来指定 notepad.exe 的进程并 **/t**参数来指定池标记**标记 1**并**Fred**。 创建由记事本的所有对象使用的都处理结果，**标记 1**或**Fred**池标记跟踪的情况。 该命令还使用 **/p**参数，它将保留跟踪数据，直到禁用跟踪。

```console
gflags /ro /t Tag1;Fred /i Notepad.exe /p
```

当用户提交该命令时，Gflags 在注册表中存储的信息。 但是，由于注册表设置不是有效的直到重新启动计算机，此对象引用跟踪已配置，但尚未开始。

Gflags 响应通过打印以下消息：

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

该消息指示，在注册表中启用对象引用跟踪。 "永久 Traces"指示关闭或重新启动计算机之前将保留跟踪数据。 池标记和要跟踪的图像文件名称，还列出了该消息。

### <a name="span-iddisplaytheobjectreferencetracingconfigurationspanspan-iddisplaytheobjectreferencetracingconfigurationspandisplay-the-object-reference-tracing-configuration"></a><span id="display_the_object_reference_tracing_configuration"></span><span id="DISPLAY_THE_OBJECT_REFERENCE_TRACING_CONFIGURATION"></span>显示跟踪配置的对象引用

您可以显示当前有效存储或存储在注册表中重新启动计算机时要使用的对象引用跟踪配置。

在此示例中，没有存储在注册表中的一个对象引用跟踪配置，另一个为运行时配置。 运行时跟踪会立即开始 （和覆盖任何注册表设置）。 但是，如果重新启动系统，运行时间设置都将丢失，并且对象引用跟踪会话注册表设置才会生效。

下面的命令显示的运行的时对象引用跟踪配置。 它使用 **/ko**不带任何其他参数的参数。

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

如果对象引用已启用跟踪，因为它是在此示例中，将显示的设置描述正在进行的跟踪。

下面的命令显示存储在注册表中的对象引用跟踪配置数据。 它使用 **/ro**不带任何其他参数的参数。

```console
gflags /ro
```

在响应中，Gflags 显示存储在注册表中的数据：

```console
Boot Registry Settings :
Object Ref Tracing Enabled
        Permanent Traces
        Pool Tags: Tag1;Fred
        Process Name: Notepad.exe
```

如果由于对象引用跟踪配置添加到注册表，已重新启动计算机，以响应 gflags /ro 命令显示的设置描述正在进行的跟踪。 但是，如果你具有尚未重新启动，或者你具有重新启动，但然后开始运行时对象引用跟踪 (**/ko**)，存储在注册表中的设置不是当前有效，但它们将再次变得有效当您重新启动系统。

### <a name="span-iddisableobjectreferencetracingspanspan-iddisableobjectreferencetracingspandisable-object-reference-tracing"></a><span id="disable_object_reference_tracing"></span><span id="DISABLE_OBJECT_REFERENCE_TRACING"></span>禁用对象引用跟踪

如果禁用运行时 （内核标志） 对象引用跟踪设置，跟踪会立即停止。 禁用注册表中的对象引用跟踪设置后，跟踪将停止时重新启动计算机。

以下命令禁用运行时对象引用跟踪。 它使用 **/d**参数来禁用所有设置。 不能禁用设置有选择地。

```console
gflags /ko -d
```

如果命令成功，Gflags 做出响应并显示以下消息：

```console
Running Kernel Settings :
Object Ref Tracing Disabled
```

以下命令禁用运行时对象引用跟踪。

以下命令禁用注册表中的对象引用跟踪设置。 它使用 **/d**参数来禁用所有设置。 不能禁用设置有选择地。 当重新启动计算机时，此命令才有效。

```console
gflags /ro -d
```

如果命令成功，Gflags 做出响应并显示以下消息：

```console
Boot Registry Settings :
Object Ref Tracing Disabled
```

 

 





