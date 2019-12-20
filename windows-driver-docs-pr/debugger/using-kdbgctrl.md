---
title: 使用 KDbgCtrl
description: 使用 KDbgCtrl
ms.assetid: 386e8861-dd55-440c-9309-7e8cf6c27690
keywords:
- KDbgCtrl
- KDbgCtrl，基本用法
- DbgPrint buffer，更改缓冲区大小
- DbgPrint buffer，KDbgCtrl 实用工具
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: c85a8138f6fceaadcbb8340123cbc198ac992afb
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209655"
---
# <a name="using-kdbgctrl"></a>使用 KDbgCtrl


可以使用 KDbgCtrl （内核调试控制、KDbgCtrl）工具从目标计算机控制内核调试连接。

若要使用此工具，目标计算机必须运行 Windows Server 2003 或更高版本的 Windows。

KDbgCtrl 可以控制五个不同的设置：完整内核调试、自动内核调试、用户模式错误处理、阻止内核调试，以及 DbgPrint 缓冲区的大小。

若要使用 KDbgCtrl，必须先在目标计算机的启动设置中启用了内核调试，然后才能进行上一次启动。 如果未执行此操作，则不能使用 KDbgCtrl 来启用内核调试。 有关这些启动设置的详细信息，请参阅[启动参数以启用调试](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-enable-debugging)。

### <a name="span-idfull_kernel_debuggingspanspan-idfull_kernel_debuggingspanfull-kernel-debugging"></a><span id="full_kernel_debugging"></span><span id="FULL_KERNEL_DEBUGGING"></span>完全内核调试

启用完全内核调试后，在主计算机上运行的内核调试器可能会侵入目标计算机。 如果遇到内核模式异常，则目标计算机将进入内核调试器。 还允许从目标到主机的消息，如**DbgPrint**输出、符号加载消息和重定向的用户模式调试器。

如果禁用此设置，则目标将忽略主机的所有信号。

默认情况下启用完全内核调试。 若要检查当前设置值，请使用**kdbgctrl-c**。 若要禁用此设置，请使用**kdbgctrl-d**。 若要启用此设置，请使用**kdbgctrl-e**。

如果希望检查当前设置，并使用它来控制批处理文件中的执行，则可以使用**kdbgctrl-cx**命令。 有关此命令的详细信息，请参阅[**KDbgCtrl 命令行选项**](kdbgctrl-command-line-options.md)。

### <a name="span-idautomatic_kernel_debuggingspanspan-idautomatic_kernel_debuggingspanautomatic-kernel-debugging"></a><span id="automatic_kernel_debugging"></span><span id="AUTOMATIC_KERNEL_DEBUGGING"></span>自动内核调试

如果启用了完全内核调试，则自动内核调试的当前设置为重要--允许所有通信。

禁用完全内核调试并启用自动内核调试后，只有目标计算机才能启动调试连接。

在这种情况下，只有内核模式异常、断点或其他内核模式事件将导致建立连接。 不会为**DbgPrint**输出、符号加载消息、重定向用户模式调试器输入和输出或其他类似消息建立连接，它们将存储在 DbgPrint 缓冲区中，而不是发送到内核调试器。

如果异常或事件导致目标进入内核调试器，则会自动打开完整内核调试，就像您已执行**kdbgctrl-e**一样。

默认情况下禁用自动内核调试（尽管这是重要，除非还禁用了完全内核调试）。 若要检查当前设置值，请使用**kdbgctrl**。 若要禁用此设置，请使用**kdbgctrl**。 若要启用此设置，请使用**kdbgctrl-ea**。

### <a name="span-iduser_mode_error_handlingspanspan-iduser_mode_error_handlingspanuser-mode-error-handling"></a><span id="user_mode_error_handling"></span><span id="USER_MODE_ERROR_HANDLING"></span>用户模式错误处理

当启用用户模式的错误处理时，某些用户模式事件将导致目标计算机进入内核调试器。

具体而言，所有**int 3**中断（例如由调试器或调用**DbgBreakPoint**插入到代码中的断点）都将导致内核调试器中断。 不过，通常不会将标准异常（如访问冲突和被零除）发送到内核调试器。

如果用户模式调试器已附加到进程，此调试器将捕获所有用户模式错误，并且不会 alterted 内核调试器。 有关各种用户模式错误处理程序的优先排名，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

要使用户模式错误处理正常工作，还必须启用完全内核调试或自动内核调试。

默认情况下，将启用用户模式错误处理。 若要检查当前设置值，请使用**kdbgctrl**。 若要禁用此设置，请使用**kdbgctrl**。 若要启用此设置，请使用**kdbgctrl-eu**。

### <a name="span-idblocking_kernel_debuggingspanspan-idblocking_kernel_debuggingspanblocking-kernel-debugging"></a><span id="blocking_kernel_debugging"></span><span id="BLOCKING_KERNEL_DEBUGGING"></span>阻止内核调试

在某些情况下，你可能想要设置目标计算机进行内核调试，但等待启用内核调试，直至目标计算机启动。 可以通过阻止内核调试来实现此目的。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

若要阻止内核调试，请使用与以下命令相似的命令来设置目标计算机：

```console
bcdedit /debug on
bcdedit /dbgsettings 1394 channel:32 /start DISABLE /noumex
```

当你重新启动目标计算机时，它将为内核调试做好准备，但会禁用内核调试和用户模式错误处理。 此时，主计算机将无法连接到目标计算机，并且内核调试器将不会捕获 bug 检查，用户模式异常将不会导致内核调试器中断。

准备就绪后，可以通过输入以下命令来启用内核调试（无需重启目标计算机）。

```console
kdbgctrl -db
kdbgctrl -e
```

稍后，你可以通过输入以下命令来禁用内核调试。

```console
kdbgctrl -d
kdbgctrl -eb
```

你可以使用**kdbgctrl-cb**来检查内核调试是否被阻止。

### <a name="span-idthe_dbgprint_buffer_sizespanspan-idthe_dbgprint_buffer_sizespanthe-dbgprint-buffer-size"></a><span id="the_dbgprint_buffer_size"></span><span id="THE_DBGPRINT_BUFFER_SIZE"></span>DbgPrint 缓冲区大小

DbgPrint 缓冲区存储目标计算机已发送到内核调试器的消息。

如果启用了完全内核调试，则这些消息将自动显示在内核调试器中。 但如果禁用此选项，则这些消息将存储在缓冲区中。 在稍后的时间点，你可以启用内核调试，连接到内核调试器，并使用[**！ dbgprint**](-dbgprint.md)扩展来查看此缓冲区的内容。 有关此缓冲区的详细信息，请参阅 DbgPrint 缓冲区。

DbgPrint 缓冲区的默认大小在 Windows 的免费版本中为 4 KB。 若要确定当前的缓冲区大小，请使用**kdbgctrl-cdb**。 若要更改缓冲区大小，请使用 **kdbgctrl * * * size*，其中*size*指定新的缓冲区大小。 有关语法的详细信息，请参阅[**KDbgCtrl 命令行选项**](kdbgctrl-command-line-options.md)。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

若要显示所有当前设置，请使用以下命令：

```console
kdbgctrl -c -ca -cu -cb -cdb 
```

若要还原默认设置，请使用以下命令：

```console
kdbgctrl -e -da -eu -db -sdb 0x1000 
```

若要锁定主机以便仅在出现异常时联系该计算机，请使用以下命令：

```console
kdbgctrl -d -ea -eu 
```

若要禁用所有内核调试，请使用以下命令：

```console
kdbgctrl -d -da 
```

如果要禁用所有内核调试，可能还需要增加 DbgPrint 缓冲区的大小。 这可确保保存所有消息，以备以后查看。 如果有兆字节的内存可用于备用，可以使用以下命令：

```console
kdbgctrl -sdb 0x100000 
```

 

 





