---
title: 调试打印机驱动程序组件
description: 调试打印机驱动程序组件
ms.assetid: 550cc8fe-5520-4521-8c4e-9c8c80521357
keywords:
- 调试驱动程序 WDK 打印机
- 打印机驱动程序 WDK，调试
- 用户模式调试 WDK 打印机
- 宏 WDK 打印机
- 全局变量 WDK 调试
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: e547a240d9b0cc6ab3bd1c9a425a2ea7bc1b7d13
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216816"
---
# <a name="debugging-printer-driver-components"></a>调试打印机驱动程序组件

如果要开发打印机驱动程序呈现插件或用户界面插件，可以在这些组件中启用调试消息。 如 "全局调试变量" 一节中所述，可以使用全局调试变量控制调试器窗口中显示的消息的详细级别。

您可以使用在 "调试消息宏" 部分中讨论的宏，在各种条件下向调试器窗口发送消息。 此外，还可以使用此部分中的信息在 Microsoft 通用打印机驱动程序中启用调试消息 (Unidrv) 或 PostScript 打印机驱动程序 (Pscript) 呈现器，前提是已选中这些 Dll 的版本。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

以下两节包含调试用户模式驱动程序和一些常规调试提示的步骤。

## <a name="preparing-for-user-mode-debugging"></a>准备用户模式调试

若要开始调试打印机驱动程序及其组件：

1. 安装最新的调试工具。 请参阅 [下载适用于 Windows 的调试工具](../debugger/debugger-download-tools.md)

1. 从[Windows 符号包](../debugger/debugger-download-symbols.md)安装正确的符号

> [!NOTE]
> 使用最新版本的调试器非常重要。

建议仅安装对调试感兴趣的组件的已检查生成。 通常会将以下零售二进制文件替换为其对应的已选中版本：

- Unidrv.dll

- Unidrvui.dll

- Unires.dll

还应安装 Oemuni 示例或正在调试的打印机驱动程序的已检查版本。 使用此方法（而不是安装整个已检查的生成系统）的优点是不会降低整个系统的速度。

## <a name="starting-a-user-mode-debugging-session"></a>启动用户模式调试会话

若要开始用户模式调试，请在 Windbg 调试器中的 " **文件** " 菜单上选择 " **附加到进程**"。 您将调试器附加到的过程取决于您尝试调试的方案。 对于打印机驱动程序，必须将调试器附加到打印应用程序或后台处理程序进程 ( # A0) 。 请记住，打印应用程序加载配置/用户界面模块，而后台处理程序进程加载呈现模块。 但是，"文件：" 打印存在差异，因此不会进行后台打印，因此，打印应用程序也会加载呈现模块。 因此，你必须确保附加到正确的进程。

> [!NOTE]
> 用户模式调试不需要两个单独的计算机。

以下过程将使你可以调试 Oemuni 示例。

1. 在 "FILE：" 端口上安装 Oemuni 示例。

1. 通过依次单击 " **开始** " 菜单、" **所有程序**"、" **附件**"，然后选择 " **写字板**"，启动 "写字板" 应用程序。

1. 在 "WinDbg **文件** " 菜单上，选择 " **附加到进程**"。 在可用进程列表中，选择 " **WordPad.exe**"。

1. 从写字板启动打印作业。 你现在已准备好调试 Oemuni 示例。

可以通过打开 giDebugLevel 变量来启用详细调试。 其默认值为3，表示警告。 如果设置为1，则表示详细。 若要用 Unidrv.dll 设置后一个值，请在调试器中键入以下命令：

```cmd
> ed unidrv!giDebugLevel 1
```

运行 Oemuni 示例时，还会应用相同的调试变量，因此若要启用详细调试，请键入以下命令：

```cmd
> ed oemuni!giDebugLevel 1
```

你还可以将自己的 debug 语句添加到 Oemuni 示例。

有关设置调试值的详细信息，请参阅 WinDbg 文档，其中描述了设置用户模式调试所需的可用命令和概述步骤。 若要访问文档，请在 WinDbg 的 " **帮助** " 菜单上选择 " **内容**"。

## <a name="global-debug-variable"></a>全局调试变量

GiDebugLevel 全局变量由 Oemui 和 Oemuni 示例在其 Debug.exe 和 Debug .cpp 文件中声明。 可以通过以下方式修改 giDebugLevel 的值：

- 在调试器中更改其值
- 在插件中重新定义其值

可以将 giDebugLevel 设置为以下任意值：

```cpp
#define DBG_VERBOSE 1
#define DBG_TERSE   2
#define DBG_WARNING 3
#define DBG_ERROR   4
#define DBG_RIP     5
```

## <a name="debug-message-macros"></a>调试消息宏

以下宏用于调试目的。 其中的几个只在 giDebugLevel 全局变量（控制发出的调试消息）设置为特定值时才采取措施。 宏在免费版本中展开为空格。 下面简要说明了它们的作用及其参数。

**断言** (*导线*) 

- 验证 *导线* 中的布尔表达式是否为 **TRUE**。 如果不是，则宏强制断点。

**ASSERTMSG** (*导线* (*msg*) # A3

- 验证 *导线* 中的布尔表达式是否为 **TRUE**。 如果不是，则宏将在 msg 中显示消息 *，* 并强制执行断点。

**ERR** ( # B1 *Msg*) # A3

- 如果当前调试级别为 = DBG 错误，则在 *msg* 中显示消息 &lt; \_ 。 消息格式为：

    ```cpp
    ERR filename (linenumber): msg
    ```

**RIP** ( # B1 *Msg*) # A3

- 在 *msg* 中显示消息，并强制断点。

**简要** ( # B1 *Msg*) # A3

- 如果当前调试级别为 = DBG 简要，则在 *msg* 中显示消息 &lt; \_ 。

**详细** ( # B1 *Msg*) # A3

- 如果当前调试级别为，则在 *msg* 中显示消息 &lt; \_ 。

**警告** ( # B1 *Msg*) # A3

- 如果当前调试级别为 = DBG 警告，则在 *msg* 中显示消息 &lt; \_ 。 消息格式为：

    ```cpp
    WRN filename (linenumber): msg
    ```

请注意，具有 *msg* 参数的所有宏都需要在此参数的前后使用一对括号。 下面是两个示例，用于说明这一要求：

```cpp
ASSERTMSG(x > 0, ("x is less than 0\n"));
```

```cpp
WARNING( ("App passed NULL pointer, ignoring...\n") );
```

包含 *msg* 参数的宏由 Oemui 和 Oemuni 示例在其 debug.exe 标头中定义。