---
title: UMDF 如何处理驱动程序故障
description: 本主题介绍在 UMDF 驱动程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统采取的操作。 它适用于 UMDF 版本1和2。
ms.assetid: 1811f131-6a51-4e53-bc8d-da511619f6fd
keywords:
- 用户模式驱动程序框架 WDK，驱动程序故障
- UMDF WDK，驱动程序故障
- 用户模式驱动程序 WDK UMDF，驱动程序故障
- 失败的驱动程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b20937877451e67a6dd00c0a4381a22035225af6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190481"
---
# <a name="how-umdf-handles-driver-failures"></a>UMDF 如何处理驱动程序故障


本主题介绍在 UMDF 驱动程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统采取的操作。 它适用于 UMDF 版本1和2。

以下事件按显示的顺序发生：

-   操作系统 (*WUDFRd.sys*) 通知反射器。

-   反射器跟踪主机进程中的未完成 i/o：
    -   反射器完成未完成的 i/o，状态 \_ 驱动程序 \_ 进程 \_ 终止错误代码。
    -   Microsoft Win32 应用程序 \_ \_ \_ 为未完成的 I/o 接收错误驱动程序进程终止错误代码。

    **注意**   在 Microsoft Windows XP 上运行的反射器完成了具有状态 \_ 驱动程序内部错误的未完成 i/o \_ \_ ，而 Win32 应用程序又接收 \_ 未完成 I/o 的错误 IO \_ 设备错误代码。 因此，在 Windows XP 上运行的应用程序不应使用错误 \_ IO \_ 设备检测驱动程序故障，因为它们不能确定从典型 i/o 请求返回的状态的任何差异 (例如，通过调用 Win32 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数返回的状态) 。

     

-   在操作系统报告主机进程的问题后，反射器会将 GUID \_ WUDF \_ 设备 \_ 主机 \_ 问题自定义即插即用 (PnP) 事件发送到操作系统。

    如果应用程序之前调用 Win32 **RegisterDeviceNotification** 函数为设备注册 GUID \_ WUDF \_ 设备 \_ 主机 \_ 问题，则该应用程序将 \_ 在主机进程失败时收到 DBT CUSTOMEVENT 通知。 有关 **RegisterDeviceNotification** 和 DBT CUSTOMEVENT 的详细信息 \_ ，请参阅 Windows SDK 文档。

-   操作系统会将一个条目写入系统事件日志，该日志指示驱动程序失败。 它还指示操作系统重启驱动程序的次数。 操作系统将以下事件编号写入系统事件日志，以指示指定的问题：

    -   如果主机进程出现错误，则为10110
    -   如果设备脱机并重新启动，则为10111
    -   10112如果设备处于脱机状态并且未重新启动

    框架可以尝试重新启动失败的驱动程序。 UMDF 代码验证程序提供了一个 [注册表值](using-umdf-verifier.md) ，用于控制重试的次数。 如果用户禁用并启用设备设备管理器或断开，并插入设备，则操作系统会创建设备的新实例，并且框架将重置重新启动计数器。

-   操作系统将内核驱动程序卸载到设备堆栈中。

    **注意**   在旧堆栈的所有句柄都关闭之前，操作系统将不会关闭并重新启动设备堆栈。 应用程序将检测设备故障以及设备 (DBT REMOVEDEVICEPENDING) 的意外删除通知 \_ 。 但是，如果旧堆栈的任何句柄保持打开状态，则不会重新启动设备。

     

-   驱动程序管理器重新启动或禁用该设备。 如果设备处于禁用状态，则操作系统会在设备管理器中显示黄色感叹号。

请注意，在 UMDF 驱动程序出现故障后，可以按任意顺序执行以下操作：

-   操作系统泪水关闭并重新启动设备。

-   反射器将 GUID \_ WUDF \_ 设备 \_ 主机 \_ 问题 PnP 事件发送到操作系统。

-   反射器完成未完成的 i/o，状态 \_ 驱动程序 \_ 进程已 \_ 终止。

因此，在操作系统重新启动设备之后，应用程序可能会收到 \_ \_ \_ 针对未完成 I/O 终止的错误驱动程序进程。 接收到错误 \_ 驱动程序 \_ 进程 \_ 终止后，该应用程序可能还会收到 \_ 由 GUID \_ WUDF \_ 设备 \_ 主机 \_ 问题事件引起的 DBT CUSTOMEVENT 通知。

 

