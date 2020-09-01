---
title: 用于测试 WMI 驱动程序支持的常规方法
description: 用于测试 WMI 驱动程序支持的常规方法
ms.assetid: 4d1a9198-2cc7-491d-a803-80f846882a6e
keywords:
- WMI WDK 内核，测试
- 测试 WMI 支持 WDK 内核
- WMI WDM 提供程序日志 WDK
- 错误 WDK WMI
- 提供程序记录 WDK WMI
- 事件 WDK WMI
- WMI WDK 内核，错误
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b32fbe906d8bfa9191463373f556037ad0c2fafd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183880"
---
# <a name="general-techniques-for-testing-wmi-driver-support"></a>用于测试 WMI 驱动程序支持的常规方法





### <a name="wmi-client-tools"></a>WMI 客户端工具

您可以使用多种工具在您的驱动程序中测试 WMI 支持。

<a href="" id="wbemtest"></a>Wbemtest  
操作系统包括 Wbemtest 工具，该工具提供了一个 GUI，可用于查询 WMI 类和类实例、更改属性值、执行方法和接收事件通知。 连接到 "根 \\ wmi" 命名空间来测试驱动程序的支持。

<a href="" id="wmic"></a>Wmic.exe  
Microsoft Windows XP 和更高版本的操作系统包含 Wmic 工具，该工具提供了一个命令行界面，可用于发出 WMI 相关命令来测试驱动程序。

<a href="" id="wmimofck"></a>Wmimofck  
**Wmimofck**命令可用于检查二进制 MOF 文件的语法。 还可以使用 **wmimofck-t** 命令生成 VBScript 文件。 你可以使用此脚本来测试驱动程序的 WMI 类实例查询的处理。 **Wmimofck**命令生成可测试查询和设置类、执行方法和接收事件的网页。 请注意，网页不支持执行使用复杂参数或返回值的方法， (如) 的嵌入类的数组。 在这种情况下，可以改为使用 Wbemtest。 有关 Wmimofck 的详细信息，请参阅 [使用 wmimofck.exe](using-wmimofck-exe.md) 。

还可以通过使用 WMI 用户模式 API 编写自定义 WMI 客户端应用程序来测试驱动程序的 WMI 支持。

有关此用户模式 API 的详细信息，允许应用程序提供或使用 WMI 信息，请参阅 Microsoft Windows SDK 文档中的 Windows Management Instrumentation 信息。

WMI 客户端应用程序执行以下任务来测试驱动程序：

-   连接到 WMI。

    若要连接到 WMI，应用程序可以调用组件对象模型 (COM) 函数 **CoCreateInstance**来检索指向 **IWbemLocator** 接口的指针。 然后，应用程序会调用 **IWbemLocator：： ConnectServer** 方法连接到 WMI。 通过此调用，应用程序将收到指向 **IWbemServices** 接口的指针。

-   访问驱动程序中的信息。

    若要访问信息并注册事件，应用程序需要使用 **IWbemServices** 接口的方法。

### <a name="wmi-irps-and-the-system-event-log"></a><a href="" id="ddk-wmi-irps-and-the-system-event-log-kg"></a>WMI Irp 和系统事件日志

严格发生在内核模式下的 WMI 错误将记录到系统事件日志中。 您可以使用事件查看器来检查系统事件日志。 有关详细信息，请 (参阅 [日志记录错误](logging-errors.md) 。 ) 

此类错误的两个主要原因是错误地回复了 WMI 请求，并对事件通知的参数不正确。 例如，如果驱动程序返回了格式不正确的 [**WMIREGINFO**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow) 数据结构来响应 [**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**IRP \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求，系统会将该数据记录到系统事件日志中。 系统还会记录对 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) 和 [**WmiFireEvent**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent) 的无效调用，以发出 WMI 事件通知。

### <a name="wmi-wdm-provider-log"></a><a href="" id="ddk-wmi-wdm-provider-log-kg"></a>WMI WDM 提供程序日志

Wmi wdm 提供程序正在处理的 WMI 错误 ( # A0) 记录到 WMI WDM 提供程序的日志文件 Wmiprov。 这是一个文本文件，可在% windir% \\ system32 \\ wbem 日志中 \\ 找到 \\ wmiprov。 此处记录了错误，如驱动程序的 MOF 资源错误或缺失。 如果 MOF 资源错误，文件% windir% \\ system32 \\ mofcomp.exe 可能具有与该错误相关的其他信息。

在早于 Windows Vista 的 Windows 版本中，你可以使用 Wmimgmt.msc 应用程序更改所有 WMI 提供程序的日志记录设置。  (在 Windows 98/Me 中，请改用 Wbemcntl。 ) 你可以禁用或重新启用日志记录、更改 WMI 日志文件的保留目录以及设置此类文件的最大大小。 有关详细信息，请参阅 [WMI 日志文件](/windows/desktop/WmiSdk/wmi-log-files)。

 

