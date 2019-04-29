---
title: 用于测试 WMI 驱动程序支持的常规方法
description: 用于测试 WMI 驱动程序支持的常规方法
ms.assetid: 4d1a9198-2cc7-491d-a803-80f846882a6e
keywords:
- WMI WDK 内核测试
- 测试 WMI 支持 WDK 内核
- WMI WDM 提供程序日志 WDK
- WDK WMI 错误
- 提供程序记录 WDK WMI
- WDK WMI 事件
- WMI WDK 内核错误
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f6c326a43b9c5dbef7029d6cbb1d382d2590bc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359946"
---
# <a name="general-techniques-for-testing-wmi-driver-support"></a>用于测试 WMI 驱动程序支持的常规方法





### <a name="wmi-client-tools"></a>WMI 客户端工具

有几种工具可用于 WMI 支持测试驱动程序中。

<a href="" id="wbemtest"></a>Wbemtest  
操作系统包括 Wbemtest 工具，它提供可用于查询 WMI 类和类实例，更改属性值、 执行方法，并接收事件通知的 GUI。 连接到"根\\wmi"命名空间以测试您的驱动程序支持。

<a href="" id="wmic"></a>Wmic  
Microsoft Windows XP 和更高版本操作系统包括 Wmic 工具，它提供了可用于发出与 WMI 相关命令，以测试您的驱动程序的命令外壳。

<a href="" id="wmimofck"></a>Wmimofck  
**Wmimofck**命令可用来检查二进制的 MOF 文件的语法。 此外可以使用**wmimofck t**命令以生成 VBScript 文件。 此脚本可用于测试您的驱动程序处理的 WMI 类实例查询。 **Wmimofck-w**命令生成可以测试查询和设置的类、 执行方法，并接收事件的网页。 请注意，网页不支持使用复杂的参数或返回值 （如嵌入类的一个数组） 的执行方法。 在这种情况下可以改为使用 Wbemtest。 请参阅[使用 wmimofck.exe](using-wmimofck-exe.md) Wmimofck 有关详细信息。

您还可以测试驱动程序的 WMI 支持通过编写自定义 WMI 客户端应用程序使用 WMI 用户模式 API。

详细了解此用户模式 API，它允许应用程序提供或使用 WMI 的信息，请参阅 Microsoft Windows SDK 文档中的 Windows Management Instrumentation 信息。

WMI 客户端应用程序将执行以下任务来测试驱动程序：

-   连接到 WMI。

    若要连接到 WMI，应用程序可以调用组件对象模型 (COM) 函数中， **CoCreateInstance**来检索一个指向**IWbemLocator**接口。 然后，应用程序调用**IWbemLocator::ConnectServer**方法连接到 WMI。 此调用，从应用程序接收一个指向**IWbemServices**接口。

-   访问驱动程序中的信息。

    若要访问的信息并注册事件，应用程序使用的方法**IWbemServices**接口。

### <a href="" id="ddk-wmi-irps-and-the-system-event-log-kg"></a>WMI Irp 和系统事件日志

严格地出现在内核模式下的 WMI 错误记录到系统事件日志。 可以使用事件查看器来检查系统事件日志。 (请参阅[日志记录错误](logging-errors.md)有关详细信息。)

此类错误的两个主要源是对 WMI 请求的格式不正确答复和事件通知的参数不正确。 例如，如果驱动程序返回格式不正确[ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)响应中的数据结构[ **IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)或[ **IRP\_MN\_REGINFO\_例如**](https://msdn.microsoft.com/library/windows/hardware/ff551734)请求时，系统将记录到系统事件日志。 系统还会记录到的无效调用[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)并[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)发出 WMI 事件通知。

### <a href="" id="ddk-wmi-wdm-provider-log-kg"></a>WMI WDM 提供程序日志

WMI WDM 提供程序 Wmiprov.log 下，WMI WDM 提供程序 (Wmiprov.dll) 被处理时出现 WMI 错误将记录到日志文件。 这是文本文件位于 %windir%\\system32\\wbem\\日志\\wmiprov.log。 错误，例如错误或缺少 MOF 资源的驱动程序，会在此处记录。 对于错误的 MOF 资源的文件 %windir%\\system32\\mofcomp.log 可能包含与错误相关的其他信息。

在版本的 Windows 早于 Windows Vista，您可以使用 Wmimgmt.msc 应用程序来更改所有 WMI 提供程序的日志记录设置。 (在 Windows 98 / 我，改为使用 Wbemcntl。)您可以禁用或重新启用日志记录，其中 WMI 日志文件会保留，以及设置此类文件的最大大小将目录更改。 有关详细信息，请参阅[WMI 日志文件](https://msdn.microsoft.com/library/aa394564)。

 

 




