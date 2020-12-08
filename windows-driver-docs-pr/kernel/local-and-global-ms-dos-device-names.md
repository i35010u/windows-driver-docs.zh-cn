---
title: 本地和全局 MS-DOS 设备名称
description: 本地和全局 MS-DOS 设备名称
keywords:
- MS-DOS 设备名称 WDK 内核
- 本地 MS-DOS 设备名称 WDK 内核
- 全局 MS-DOS 设备名称 WDK 内核
- DosDevices 上下文 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d08b7c9c4ad999e6e517bb59b6e4d387e763ac9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823071"
---
# <a name="local-and-global-ms-dos-device-names"></a>本地和全局 MS-DOS 设备名称

Microsoft Windows 2000 和更高版本的基于 Windows NT 的操作系统维护多个版本的 **DosDevices** 目录。

在这些操作系统中，有一个 *全局* **\\ DosDevices** 目录和多个 *本地* **\\ DosDevices** 目录。 全局 **\\ DosDevices** 目录包含系统范围内可见的 MS-DOS 设备名称。 本地 **\\ DosDevices** 目录保存仅在特定 *本地* **DosDevices** *上下文* 中可见的 MS-DOS 设备名称。

本地 **DosDevices** 上下文如下所示。

-   在 Windows XP 和更高版本中，每个登录会话都有其自己的本地 **DosDevices** 上下文。 系统线程和作为 LocalSystem 用户运行的任何线程都不会在本地 **DosDevices** 上下文中运行。

-   在 Windows 2000 上，每个终端服务器会话都有其自己的本地 **DosDevices** 上下文。 作为控制台会话的一部分运行的任何线程都不会在本地 **DosDevices** 上下文中运行。

每个线程都有当前的 **DosDevices** 上下文，该上下文可在线程的生存期内更改。 未在本地 **DosDevices** 上下文中运行的线程称为在 *全局* **DosDevices** *上下文* 中运行。 因此，系统帐户在全局 **DosDevices** 上下文中运行。

如果某个线程当前正在本地 **DosDevices** 上下文中运行，则它创建的所有 MS-DOS 设备名称只能在本地 **DosDevices** 目录中创建。 因此，在本地 **DosDevices** 上下文中运行的线程不会影响对其他本地 **DosDevices** 上下文或全局 **DosDevices** 上下文中运行的线程可见的 MS-DOS 设备名称。 例如，如果 Windows XP 或更高版本上的用户将网络驱动器作为 **X：** 装载，则这不会影响 **x：** 对于任何其他用户或整个系统的含义。

在 Windows XP 和更高版本上，当对象管理器在 **\\ DosDevices** 中查找名称时，它首先搜索本地 **\\ DosDevices** 目录，然后搜索全局 **\\ DosDevices** 目录。 如果在这两个位置都存在名称，则本地名称将隐藏全局名称。

在 Windows 2000 上，每当启动新的终端服务器会话时，系统都将 \\ 通过复制全局 **\\ DosDevices** 目录生成本地 **DosDevices** 目录。 对全局目录的任何后续更改都不会传播到本地目录。

必须在全局 **\\ DosDevices** 目录中创建其 MS-DOS 设备名称的驱动程序可以通过在标准驱动程序例程中创建其符号链接（可保证在系统线程上下文中运行，例如 **DriverEntry**）来实现此目的。 或者，全局 **\\ DosDevices** 目录作为 **\\ DosDevices \\ global** 提供; 驱动程序可以使用 **\\ DosDevices \\ global \\**<em>DosDeviceName</em>的名称指定全局目录中的名称。

请注意，不支持本地和全局版本的 **\\ DosDevices** 的平台（如 Windows 98/Me）不存在 **\\ DosDevices \\ Global** 。 下面的代码示例创建一个适用于 Windows 98/Me 以及 Windows 2000 和更高版本操作系统的全局符号链接：

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

驱动程序可以通过创建符号链接来响应 IOCTL，在本地 **\\ DosDevices** 目录中创建 MS-DOS 设备名称。 当特定本地 **DosDevices** 上下文中的线程发送 IOCTL 时，从当前线程上下文内调用驱动程序的 *DispatchDeviceControl* 。

有关运行标准驱动程序例程的上下文的详细信息，请参阅 [调度例程和 IRQLs](dispatch-routines-and-irqls.md)。

系统区分本地 **\\ DosDevices** 目录，如下所示：

-   在 Windows XP 和更高版本中，本地 **\\ DosDevices** 目录由登录会话的访问令牌的 **AuthenticationID** 标识。 有关 **AuthenticationID** 的详细信息，请参阅 Microsoft Windows SDK 文档中的 **令牌 \_ 统计信息** 结构的描述。

-   在 Windows 2000 上，本地 **\\ DosDevices** 目录由终端服务器会话的 **SessionId** 标识。 有关 **SessionId** 的详细信息，请参阅 Windows SDK 文档中的 **WTS \_ 会话 \_ 信息** 结构的描述。

Windows NT 4.0 Terminal Server Edition 支持的本地 \\ **DosDevices** 目录的方式与 Windows 2000 完全相同。

 

 




