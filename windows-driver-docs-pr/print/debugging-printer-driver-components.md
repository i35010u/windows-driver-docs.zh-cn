---
title: 调试打印机驱动程序组件
description: 调试打印机驱动程序组件
ms.assetid: 550cc8fe-5520-4521-8c4e-9c8c80521357
keywords:
- 调试驱动程序 WDK 打印机
- 打印机驱动程序 WDK，调试
- 用户模式下调试 WDK 打印机
- 宏 WDK 打印机
- 全局变量 WDK 调试
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2fbe2ad35d80877ba3ebe3c1ef94c1bb581f3483
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564551"
---
# <a name="debugging-printer-driver-components"></a>调试打印机驱动程序组件

如果你正在开发呈现插件的打印机驱动程序或插件的用户界面，可以启用这些组件中的调试消息。 调试的全局变量节中所述，可以使用全局调试变量来控制在调试器窗口中显示的消息中的详细信息的级别。

调试消息宏节所述的宏可用于将消息发送到各种条件下在调试器窗口。 此外，您可以使用本部分中的信息可在 Microsoft 通用打印机驱动程序 (Unidrv) 或 PostScript 的打印机驱动程序 (Pscript) 呈现器的调试消息，前提是您已生成的这些 Dll。

在接下来的两部分包含用于调试的用户模式驱动程序和调试的一些常规提示的步骤。

## <a name="preparing-for-user-mode-debugging"></a>准备用于用户模式下调试

若要开始调试打印机驱动程序和其组件：

1. 安装最新调试工具。 请参阅[下载 Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)

1. 安装从正确的符号[Windows 符号包](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)

> [!NOTE]
> 它是调试器的非常重要，使用最新版本。

最好安装仅您感兴趣调试的组件的内部的版本。 通常您会替换为以下发布二进制文件及其相应的检查内部版本号：

- Unidrv.dll
- Unidrvui.dll
- Unires.dll

此外应安装 Oemuni 示例数据还是正在调试的打印机驱动程序的内部的版本。 使用这种方法，而不是安装整个已检验的版本系统的优点是不会减慢整个系统。

## <a name="starting-a-user-mode-debugging-session"></a>启动用户模式下调试会话

若要开始调试用户模式下，在**文件**在 Windbg 调试器中，选择菜单**附加到进程**。 附加到调试器的过程取决于您尝试调试的方案。 对于打印机驱动程序，必须将调试器附加到的打印应用程序或到后台处理程序处理 (Spoolsv.exe)。 请记住，打印应用程序加载配置/用户界面模块，而后台进程将加载呈现模块。 但是，有的差异"文件:"打印后台处理不会发生，其中的打印应用程序的结果，还加载呈现模块。 因此，您必须确保附加到正确的进程。

> [!NOTE]
> 用于用户模式下调试不需要两个单独的计算机。

以下过程将帮助你准备好调试 Oemuni 示例。

1. 将 Oemuni 示例安装在"文件:"端口。
1. 通过单击启动写字板应用程序**启动**菜单中，选择**所有程序**，选择**附件**，然后选择**写字板**.
1. 在 WinDbg**文件**菜单中，选择**附加到进程**。 在可用进程的列表中选择**WordPad.exe**。
1. 从写字板中启动打印作业。 现在您就可以调试 Oemuni 示例。

您可以启用详细调试开启 giDebugLevel 变量。 其默认值为 3，该项表示警告。 如果设置为 1，则表示详细。 若要设置 Unidrv.dll 与第二个值，请在调试器中键入以下命令：

```cmd
> ed unidrv!giDebugLevel 1
```

时要在运行 Oemuni 示例，同一个调试变量也适用，因此若要启用详细调试，请键入以下命令：

```cmd
> ed oemuni!giDebugLevel 1
```

您还可以向 Oemuni 示例添加您自己的调试语句。

有关调试的值设置的详细信息，请参阅 WinDbg 文档，其中介绍可用的命令，并概述了设置用户模式下调试所需的步骤。 若要访问的文档，在 WinDbg**帮助**菜单中，选择**内容**。

## <a name="global-debug-variable"></a>调试全局变量

通过其 Debug.h 和 Debug.cpp 文件中的 Oemui 和 Oemuni 示例声明 giDebugLevel 全局变量。 可以通过修改 giDebugLevel 的值：

- 在调试器中的其值更改
- 重新定义其在插件中的值

可以将 giDebugLevel 设置为以下值之一：

```cpp
#define DBG_VERBOSE 1
#define DBG_TERSE   2
#define DBG_WARNING 3
#define DBG_ERROR   4
#define DBG_RIP     5
```

## <a name="debug-message-macros"></a>调试消息宏

下列宏用于调试目的。 仅当 giDebugLevel 全局变量，发出的调试消息的控件，设置为特定值，多个执行操作。 宏扩展到空格免费生成。 以下是他们执行的操作及其参数的简要说明。

**ASSERT**(*cond*)

- 验证是否中的布尔表达式*条件*是**TRUE**。 如果不是这样，宏会强制断点。

**ASSERTMSG**(*cond,* (*msg*))

- 验证是否中的布尔表达式*条件*是**TRUE**。 如果不是这样，该宏将显示中的消息*msg，* 并强制断点。

**ERR**((*msg*))

- 显示中的消息*msg*当前的调试级别是否&lt;= DBG\_错误。 消息格式为：

    ```cpp
    ERR filename (linenumber): msg
    ```

**RIP**((*msg*))

- 显示中的消息*msg*并强制断点。

**TERSE**((*msg*))

- 显示中的消息*msg*当前的调试级别是否&lt;= DBG\_TERSE。

**VERBOSE**((*msg*))

- 显示中的消息*msg*当前的调试级别是否&lt;= DBG\_VERBOSE。

**WARNING**((*msg*))

- 显示中的消息*msg*当前的调试级别是否&lt;= DBG\_警告。 消息格式为：

    ```cpp
    WRN filename (linenumber): msg
    ```

请注意，所有与宏*msg*参数需要额外的一对括号周围此参数。 下面是两个示例，演示了这一要求：

```cpp
ASSERTMSG(x > 0, ("x is less than 0\n"));
```

```cpp
WARNING( ("App passed NULL pointer, ignoring...\n") );
```

包含的宏*msg*其 Debug.h 标头中的 Oemui 和 Oemuni 示例通过定义参数。
