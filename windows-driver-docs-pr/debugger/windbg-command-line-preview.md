---
title: WinDbg 预览版 - 命令行启动选项
description: 本部分介绍 WinDbg 预览调试器的命令行启动选项。
ms.date: 09/11/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 5392ff238b143da4c38f801b9ed2cb74f9c7bd9d
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256685"
---
# <a name="windbg-preview---command-line-startup-options"></a>WinDbg 预览版 - 命令行启动选项

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png)

## <a name="starting-windbg-preview"></a>正在启动 WinDbg 预览版

安装 WinDbg Preview 后，WinDbgX 可从任何目录位置运行。

## <a name="command-line-startup-options"></a>命令行启动选项

```dbgsyntax
WinDbgX [options]
```

下表总结了可用的命令行选项。

**常规选项**

|     选项      |                                                                          描述                                                                          |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -c *"command"*  | 附加调试器后执行命令行。 此命令必须用引号引起来。 可以用分号分隔多个命令。 |
| -v               | 在调试器中启用详细输出。                                                            |
| -T*标题*       | 设置窗口标题。                                                                     |
| -徽标*日志文件*  | 日志打开。 开始将信息记录到日志文件。 如果该文件存在，它将被覆盖。                                |
| -loga*日志文件*  | 日志追加。 开始将信息记录到日志文件。 如果该文件存在，则会将其追加到。                               |
| -e *EventHandle* | 在目标中出现下一个异常之后，用给定句柄向事件发出信号。                                         |
|       -?         |  显示可用的命令摘要。                                                           |

**内核选项**

|       选项       |                                                                      描述                                                                      |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| -k \[ConnectType\] | 启动内核调试会话。  如果使用 **-k**而没有任何*ConnectType*选项，则它必须是命令行中的最后一个条目。 |
|        -kqm        | 在安静模式下启动 KD。                                                                |
|        -kl         | 在调试器所在的同一台计算机上启动内核调试会话。                                         |
| -kx *ExdiOptions*  | 使用 EXDI 驱动程序启动内核调试会话。                                                |
|         -d         | 重新启动后，只要加载内核模块，调试器就会进入目标计算机。                         |

**用户模式选项**

选项 | 描述
|------ | -----------|
-o | 调试由目标应用程序启动的所有进程（子进程）。 
-g | 忽略目标应用程序中的初始断点。 
-G |忽略目标应用程序中的最终断点。 
-pv | 指定调试器应附加到目标进程 noninvasively。
-hd | 指定不应使用调试堆。
-cimp | 指定创建的任何进程都将使用服务器设置的隐式命令行，而不是客户端提供的用户指定的命令行字符串。

**目标选项**

| 选项                     |                 描述                                                                                                                                  |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -remote *ClientTransport*  | 连接到已在运行的调试服务器。 有关可能的*ClientTransport*值的说明，请参阅[激活调试客户端](activating-a-debugging-client.md)。 使用此参数时，该参数必须是命令行中的第一个参数。 |
| -server *ServerTransport*  | 创建可由其他调试器访问的调试服务器。 有关可能的*ServerTransport*值的说明，请参阅[激活调试服务器](activating-a-debugging-server.md)。              |
| -premote *SmartClientTransport*   | 创建智能客户端，并连接到已在运行的进程服务器。 有关可能的 SmartClientTransport 值的说明，请参阅[激活智能客户端](activating-a-smart-client.md)。 |
| -p *PID*               | 指定要调试的十进制进程 ID。                                                                                                              |
| -tid *tid*             | 指定在启动调试会话时要恢复的线程的线程 ID。                                                                      |
| -psn *ServiceName*     | 指定要调试的进程中包含的服务的名称。 这用于调试已经在运行的进程。                           |
| -pn *ProcessName*      | 指定要调试的进程的名称。                                                                                                             |
| -z *DumpFile*          | 指定要调试的故障转储文件的名称。 如果路径和文件名包含空格，则必须用引号将其引起来。                       |
| -debugArch x86 或 amd64    | 重写自动检测行为并为调试器设置目标位数。                                                                           |
| -loadSession           | 加载已保存的会话配置文件。                                                                                                                      |
| -setupFirewallRules    | 在本地系统上配置所需的防火墙规则，以允许使用 KDNET 进行内核调试。                                                                         |
| -openPrivateDumpByHandle*句柄* | *仅限 Microsoft 内部使用*。 指定要调试的故障转储文件的句柄。                                                                 |
| -benchmarkStartup      | *仅限 Microsoft 内部使用*。 运行启动基准并将结果追加到文件。                                                                                                    |

**符号选项**

选项 | 描述
|------ | -----------|
-y *SymbolPath* | 指定要使用的符号路径。 使用分号（ **;** ）分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息和更改此路径的其他方式，请参阅[符号路径](symbol-path.md)。
-n              | 干扰符号加载。 从符号处理程序启用详细输出。
-i *ImagePath*  | 设置要使用的图像搜索路径。
-sdce           | 使调试器在符号加载过程中显示 "文件访问错误" 消息。
-ses            | 使调试器对所有符号文件执行严格的评估，并忽略任何有问题的符号。
-sicv           | 使符号处理程序忽略 CV 记录
-问题           | 导致调试器忽略符号路径和可执行图像路径环境变量。
-snc            | 使调试器关闭C++转换。
-snul           | 为非限定名称禁用自动符号加载。
-sup            | 使符号处理程序在每个符号搜索过程中搜索公共符号表
-sflags         | 同时设置所有符号处理程序选项。

**源路径选项**

 选项   | 描述
|-------- | -----------|
-srcpath  | 指定要在调试服务器上使用的源路径。
-lsrcpath | 指定要在本地客户端上使用的源路径。

如果你在本地调试器会话中，srcpath 和 lsrcpath 实际上是相同的（"服务器" 是你的本地会话）。 对于远程调试，你可能需要将这些值设置为不同的值 situtations。 有关远程调试的详细信息，请参阅[远程调试](remote-debugging.md)。

**异常处理**

选项 | 描述
|------ | -----------|
-x   |   仅对访问冲突异常启用第二次处理。
-xe*异常*  |   为指定的异常启用第一次异常处理。
-xd*异常* |   为指定的异常启用第二次异常处理。
-xn*异常* |   对于给定的异常，禁用第一次和第二次处理，并仅在控制台上显示一条消息。
-xi*异常* |   完全忽略给定的异常，禁用第一次和第二次处理，而不将任何内容输出到控制台。

有关可以指定的异常的列表，请参阅[事件定义和默认值](https://docs.microsoft.com/windows-hardware/drivers/debugger/controlling-exceptions-and-events#event-definitions-and-defaults)。

**Post 事后**

选项  | 描述
|------ | -----------|
-I     | 将 WinDbg Preview 设置为系统的默认事后调试器。
-为    | 以无提示方式将 WinDbg Preview 设置为系统的默认事后调试器，只报告错误。

**弃用的选项**

选项 | 描述
|------ | -----------|
-Q   | 不推荐使用的命令行选项。
-QY  | 不推荐使用的命令行选项。
-QS  | 不推荐使用的命令行选项。
-QSY | 不推荐使用的命令行选项。
-WX  | 不推荐使用的命令行选项。

有关启动参数的常规信息，请参阅[WinDbg 命令行选项](windbg-command-line-options.md)。

您可以使用-？ 列出支持的命令行选项。

![命令行帮助的屏幕截图有关50选项的输出列表](images/windbgx-start-up-options.png)

## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
