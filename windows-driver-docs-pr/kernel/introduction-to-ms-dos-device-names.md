---
title: MS-DOS 设备名称简介
description: MS-DOS 设备名称简介
ms.assetid: 44b2f871-56e1-46d3-aab4-c38f498d089d
keywords:
- MS-DOS 设备名称 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af3eab546708499c904671148af90609e2ac36e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341458"
---
# <a name="introduction-to-ms-dos-device-names"></a>MS-DOS 设备名称简介





由非 WDM 驱动程序通常创建一个命名的设备对象中包含 MS-DOS 设备名称。 MS-DOS 设备名称是在窗体的名称的对象管理器中的符号链接 **\\DosDevices\\**<em>DosDeviceName</em>。

MS-DOS 设备名称与设备的一个示例是串行端口，COM1。 它具有 MS-DOS 设备名称 **\\DosDevices\\COM1**。 同样，C 驱动器的名称 **\\DosDevices\\c:**。

WDM 驱动程序通常不提供其设备的 MS-DOS 设备名称。 相反，使用 WDM 驱动程序[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)例程，以注册设备接口。 设备接口指定设备由各自的功能，而不是特定的命名约定。 有关详细信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)。

驱动程序需要提供 MS-DOS 设备名称，仅当设备需要具有特定的已知 MS-DOS 设备名称以使用用户模式程序。

驱动程序通过使用提供设备对象的 MS-DOS 设备名称[ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)例程，以创建到设备的符号链接。 例如，下面的代码示例创建从符号链接 **\\DosDevices\\**<em>DosDeviceName</em>到**\\设备\\**  <em>DeviceName</em>。

```cpp
UNICODE_STRING DeviceName;
UNICODE_STRING DosDeviceName;
NTSTATUS status;

RtlInitUnicodeString(&DeviceName, L"\\Device\\DeviceName");
RtlInitUnicodeString(&DosDeviceName, L"\\DosDevices\\DosDeviceName");
status = IoCreateSymbolicLink(&DosDeviceName, &DeviceName);
if (!NT_SUCCESS(status)) {
  /* Symbolic link creation failed.  Handle error appropriately. */
}
```

请注意，系统支持的多个版本 **\\DosDevices**目录。 请确保您的驱动程序在你想的版本中创建其符号链接。 有关详细信息，请参阅[本地和全局 MS-DOS 设备名称](local-and-global-ms-dos-device-names.md)。

访问**DosDevices**命名空间从用户模式下，指定 **\\ \\。\\**时打开的文件名称。 可以在用户模式下打开对应的设备，通过调用**createfile （)**。

例如，下面的代码示例将打开\\ \\DosDevices\\\\*DosDeviceName*在用户模式下的设备。

```cpp
file = CreateFileW(L"\\\\.\\DosDeviceName",
  GENERIC READ | GENERIC WRITE,
    0,
    NULL,
    OPEN_EXISTING,
    0,
    NULL);
```

符号链接也从用户模式应用程序通过使用用户模式下创建**DefineDosDevice**例程。 有关详细信息，请参阅 Microsoft Windows SDK。

 

 




