---
title: 本地和全局 MS-DOS 设备名称
description: 本地和全局 MS-DOS 设备名称
ms.assetid: bfb7e41c-0f80-4cb9-b036-d1b44473f9fb
keywords:
- MS-DOS 设备名称 WDK 内核
- 本地 MS-DOS 设备名称 WDK 内核
- 全局 MS-DOS 设备名称 WDK 内核
- DosDevices 上下文 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2014768008e5ff4bf42f4ba3544e0a9af4781068
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545917"
---
# <a name="local-and-global-ms-dos-device-names"></a>本地和全局 MS-DOS 设备名称

Microsoft Windows 2000 和更高版本的基于 Windows NT 的操作系统维护的多个版本**DosDevices**目录。

在这些操作系统上还有一个*全局*  **\\DosDevices**目录和多个*本地*  **\\DosDevices**目录。 全局 **\\DosDevices**目录包含可见的系统范围内的 MS-DOS 设备名称。 本地 **\\DosDevices**目录包含仅在特定可见的 MS-DOS 设备名称*本地* **DosDevices** *上下文*.

本地**DosDevices**上下文是按如下所示。

-   Windows XP 及更高版本，每个登录会话具有自己的本地**DosDevices**上下文。 系统线程和作为本地系统用户运行的任何线程不能运行在本地**DosDevices**上下文。

-   在 Windows 2000 上每个终端服务器会话具有自己的本地**DosDevices**上下文。 正在作为控制台会话的一部分不会在本地运行的任何线程**DosDevices**上下文。

每个线程具有当前**DosDevices**上下文，可以更改线程的生存期内。 不会在本地运行的线程**DosDevices**上下文中运行被认为*全局* **DosDevices** *上下文*。 因此，在系统帐户运行在全局**DosDevices**上下文。

如果在本地中当前正在运行线程**DosDevices**上下文中，它会创建任何 MS-DOS 设备名称创建仅在本地**DosDevices**目录。 因此，在本地运行的线程**DosDevices**上下文不会影响在另一个本地运行的线程是可见的 MS-DOS 设备名称**DosDevices**上下文或在全局**DosDevices**上下文。 例如，如果用户在 Windows XP 或更高版本装载上一个网络驱动器作为**x:**，这不会影响的含义**x:** 任何其他用户，或作为一个整体系统。

Windows XP 及更高版本，当对象管理器查找一个姓名中 **\\DosDevices**，它将先搜索本地 **\\DosDevices**目录，并全局 **\\DosDevices**目录。 如果名称存在于这两个位置，本地名称隐藏全局名称。

在 Windows 2000 上时启动新的终端服务器会话时，系统将生成本地\\ **DosDevices**通过将复制的全局目录 **\\DosDevices**目录。 本地目录的全局目录的任何后续更改不会传播。

必须在全局创建其 MS-DOS 设备名称的驱动程序 **\\DosDevices**目录可以执行操作来保证在系统线程上下文中，如运行的标准驱动程序例程中创建其符号链接**DriverEntry**。 或者，全局 **\\DosDevices**目录是可用作 **\\DosDevices\\全局**; 驱动程序可以使用的名称 **\\DosDevices\\Global\\**<em>DosDeviceName</em>全局目录中指定的名称。

请注意，  **\\DosDevices\\Global**不支持的本地和全局版本的平台上不存在 **\\DosDevices**，例如 Windows 98 / me 一起提供。 下面的代码示例创建适用于 Windows 98 的全局符号链接 / 我以及 Windows 2000 及更高版本的操作系统：

```cpp
UNICODE_STRING deviceName; // Already initialized.
UNICODE_STRING symbolicLinkName; // Initializing below.
NTSTATUS status;

if (IoIsWdmVersionAvailable(1, 0x10)) {
    // We're on Windows 2000 or later, so we use \DosDevices\Global.
 
    RtlInitUnicodeString(&symbolicLinkName, L"\\DosDevices\\Global\\SymbolicLinkName");

} else {
    // Windows 98/Me.  We just use DosDevices.
 
    RtlInitUnicodeString(&symbolicLinkName, L"\\DosDevices\\SymbolicLinkName");
}

status = IoCreateSymbolicLink(&symbolicLinkName, &deviceName);
if (!NT_SUCCESS(status)) {
  /* Symbolic link creation failed.  Handle error appropriately. */
}
```

驱动程序可以在本地创建 MS-DOS 设备名称 **\\DosDevices**通过 IOCTL 响应创建符号链接的目录。 当在特定的本地线程**DosDevices**上下文会发送 IOCTL，该驱动程序*DispatchDeviceControl*从当前线程上下文中调用。

有关运行标准驱动程序例程的上下文的详细信息，请参阅[调度例程和于 Irql](dispatch-routines-and-irqls.md)。

系统用于区分本地 **\\DosDevices**目录，如下所示：

-   在 Windows XP 和更高版本，本地 **\\DosDevices**由标识目录**AuthenticationID**登录会话的访问令牌。 有关详细信息**AuthenticationID**，请参阅的说明**令牌\_统计信息**Microsoft Windows SDK 文档中的结构。

-   在 Windows 2000 中，本地 **\\DosDevices**由标识目录**SessionId**终端服务器会话。 有关详细信息**SessionId**，请参阅的说明**WTS\_会话\_信息**Windows SDK 文档中的结构。

Windows NT 4.0 Terminal Server Edition 支持本地\\ **DosDevices**完全相同的方式为 Windows 2000 中的目录。

 

 




