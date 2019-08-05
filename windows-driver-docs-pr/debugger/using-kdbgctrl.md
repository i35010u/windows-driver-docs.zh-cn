---
title: 使用 KDbgCtrl
description: 使用 KDbgCtrl
ms.assetid: 386e8861-dd55-440c-9309-7e8cf6c27690
keywords:
- KDbgCtrl
- KDbgCtrl，基本用法
- DbgPrint 缓冲区，更改缓冲区大小
- DbgPrint 缓冲区，KDbgCtrl 实用程序
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: aa5f793c64e310947253c91ae7b8043c978dc719
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368620"
---
# <a name="using-kdbgctrl"></a>使用 KDbgCtrl


KDbgCtrl （内核调试控件、 kdbgctrl.exe） 工具可用于控制内核调试从目标计算机的连接。

若要使用此工具，在目标计算机必须运行 Windows Server 2003 或更高版本的 Windows。

KDbgCtrl 可以控制五个不同的设置：完整的内核调试、 自动内核调试，用户模式下的错误处理、 阻止的内核调试和 DbgPrint 缓冲区的大小。

若要使用 KDbgCtrl，您必须已启用的上一次启动之前对目标计算机的启动设置中的内核调试。 KDbgCtrl 不能用于启用内核调试，如果没有这样做。 请参阅[启用调试的启动参数](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-enable-debugging)的详细信息请参阅启动设置。

### <a name="span-idfull_kernel_debuggingspanspan-idfull_kernel_debuggingspanfull-kernel-debugging"></a><span id="full_kernel_debugging"></span><span id="FULL_KERNEL_DEBUGGING"></span>完整的内核调试

启用完整的内核调试后，在主计算机上运行的内核调试程序可以分解为目标计算机。 目标计算机将进入内核调试器是否命中内核模式异常。 将消息从目标到主机，如**DbgPrint**还允许输出、 符号加载消息和重定向的用户模式下调试程序。

如果此设置处于禁用状态，目标将忽略所有信号从主计算机。

默认情况下启用了完整的内核调试。 若要检查当前的设置值，请使用**kdbgctrl-c**。 若要禁用此设置，请使用**kdbgctrl-d**。 若要启用此设置，请使用**kdbgctrl-e**。

如果你想要检查的当前设置并使用它来控制批处理文件中的执行，则可以使用**kdbgctrl cx**命令。 此命令的详细信息，请参阅[ **KDbgCtrl 命令行选项**](kdbgctrl-command-line-options.md)。

### <a name="span-idautomatic_kernel_debuggingspanspan-idautomatic_kernel_debuggingspanautomatic-kernel-debugging"></a><span id="automatic_kernel_debugging"></span><span id="AUTOMATIC_KERNEL_DEBUGGING"></span>自动内核调试

如果启用了完整的内核调试，自动内核调试的当前设置并不重要--允许的所有通信。

完整的内核调试已禁用并启用了自动内核调试时，仅在目标计算机可以启动调试的连接。

在这种情况下，只有一个内核模式异常、 断点或其他内核模式事件将导致建立连接。 将未建立连接，对于**DbgPrint**输出、 符号加载消息、 重定向的用户模式调试器输入和输出或其他类似的消息-这些值而不是发送到 DbgPrint 缓冲区中存储内核调试程序。

如果异常或事件会导致目标进入内核调试器，则完整的内核调试将自动打开，就像具有执行**kdbgctrl-e**。

自动内核调试默认处于禁用状态 （尽管这是重要的除非完全内核调试已禁用）。 若要检查当前的设置值，请使用**kdbgctrl ca**。 若要禁用此设置，请使用**kdbgctrl-da**。 若要启用此设置，请使用**kdbgctrl ea**。

### <a name="span-iduser_mode_error_handlingspanspan-iduser_mode_error_handlingspanuser-mode-error-handling"></a><span id="user_mode_error_handling"></span><span id="USER_MODE_ERROR_HANDLING"></span>用户模式下的错误处理

启用用户模式下的错误处理后，某些用户模式事件将导致进入内核调试器在目标计算机。

具体而言，所有**int 3**中断-如断点插入到代码中由调试器或调用**DbgBreakPoint** -将导致进入内核调试器中断。 但是，标准异常-如访问冲突和除数为零-将通常不会发送到内核调试程序。

如果用户模式下调试器已附加到进程，此调试器将捕获所有用户模式错误，并且内核调试程序将不是 alterted。 有关各种用户模式下的错误处理程序的优先排名，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

对于用户模式错误处理函数，完整的内核调试或自动内核调试必须启用以及。

默认情况下启用用户模式下的错误处理。 若要检查当前的设置值，请使用**kdbgctrl-cu**。 若要禁用此设置，请使用**kdbgctrl-du**。 若要启用此设置，请使用**kdbgctrl 欧洲**。

### <a name="span-idblocking_kernel_debuggingspanspan-idblocking_kernel_debuggingspanblocking-kernel-debugging"></a><span id="blocking_kernel_debugging"></span><span id="BLOCKING_KERNEL_DEBUGGING"></span>阻止内核调试

在某些情况下可能想要设置目标计算机以进行内核调试，但启用内核调试之前启动目标计算机后。 通过阻止内核调试，可以执行的操作。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

若要阻止内核调试，通过使用类似于以下命令设置目标计算机：

```console
bcdedit /debug on
bcdedit /dbgsettings 1394 channel:32 /start DISABLE /noumex
```

重新启动目标计算机时，它将做好的内核调试，但将禁用内核调试和用户模式下的错误处理。 此时，主计算机将不能将附加到目标计算机、 内核调试器中，将不会捕获 bug 检查和用户模式异常到内核调试程序不会导致中断。

准备就绪后，可以启用内核调试 （无需重新启动目标计算机） 通过输入以下命令。

```console
kdbgctrl -db
kdbgctrl -e
```

更高版本，则可以禁用内核调试通过输入以下命令。

```console
kdbgctrl -d
kdbgctrl -eb
```

可以使用**kdbgctrl cb**以检查是否阻止内核调试。

### <a name="span-idthe_dbgprint_buffer_sizespanspan-idthe_dbgprint_buffer_sizespanthe-dbgprint-buffer-size"></a><span id="the_dbgprint_buffer_size"></span><span id="THE_DBGPRINT_BUFFER_SIZE"></span>DbgPrint 缓冲区大小

DbgPrint 缓冲区存储目标计算机将发送到内核调试程序的消息。

如果启用了完整的内核调试，这些消息将自动出现在内核调试程序。 但如果禁用此选项，则将在缓冲区中存储这些消息。 在一个更高版本的时间点，可以启用内核调试，连接到内核调试程序，并使用[ **！ dbgprint** ](-dbgprint.md)扩展以查看此缓冲区的内容。 有关此缓冲区的详细信息，请参阅 DbgPrint 缓冲区。

DbgPrint 缓冲区的默认大小为 4 KB 已检验版本的 Windows 上免费版本的 Windows 和 32 KB。 若要确定当前缓冲区大小，请使用**kdbgctrl cdb**。 若要更改的缓冲区大小，请使用 **kdbgctrl sdb * * * 大小*，其中*大小*指定新的缓冲区大小。 有关语法的详细信息，请参阅[ **KDbgCtrl 命令行选项**](kdbgctrl-command-line-options.md)。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

若要显示所有当前设置，请使用以下命令：

```console
kdbgctrl -c -ca -cu -cb -cdb 
```

若要还原默认设置，请使用以下命令：

```console
kdbgctrl -e -da -eu -db -sdb 0x1000 
```

若要锁定的主机计算机，以便它仅连接到的异常上，使用以下命令：

```console
kdbgctrl -d -ea -eu 
```

若要禁用所有内核调试，请使用以下命令：

```console
kdbgctrl -d -da 
```

如果要禁用所有内核调试，你可能希望增加 DbgPrint 缓冲区的大小。 这确保了在您需要查看其更高版本的情况下，将保存所有消息。 如果您有多余的内存兆字节时，可以使用以下命令：

```console
kdbgctrl -sdb 0x100000 
```

 

 





