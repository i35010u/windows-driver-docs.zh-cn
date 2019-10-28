---
title: MS-DOS 设备名称简介
description: MS-DOS 设备名称简介
ms.assetid: 44b2f871-56e1-46d3-aab4-c38f498d089d
keywords:
- MS-DOS 设备名称 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83fac0d285bcaaf5749287f7c0e387b503bf0302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838626"
---
# <a name="introduction-to-ms-dos-device-names"></a>MS-DOS 设备名称简介





非 WDM 驱动程序创建的命名设备对象通常具有 MS-DOS 设备名称。 MS-DOS 设备名称是对象管理器中名称格式为 **\\DosDevices\\** <em>DosDeviceName</em>的符号链接。

使用 MS-DOS 设备名称的设备示例是串行端口 COM1。 它具有 MS-DOS 设备名称 **\\DosDevices\\COM1**。 同样，C 驱动器的名称 **\\DosDevices\\C：** 。

WDM 驱动程序通常不为其设备提供 MS-DOS 设备名称。 相反，WDM 驱动程序使用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)例程来注册设备接口。 设备接口按其功能而不是特定的命名约定来指定设备。 有关详细信息，请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

仅当设备需要具有特定的已知 MS-DOS 设备名称才能与用户模式程序一起使用时，才需要驱动程序提供 MS-DOS 设备名称。

驱动程序通过使用[**IoCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)例程创建设备的符号链接，为设备对象提供 MS-DOS 设备名称。 例如，下面的代码示例创建一个从 **\\DosDevices\\** <em>DosDeviceName</em>到 **\\设备\\** <em>DeviceName</em>的符号链接。

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

请注意，系统支持 **\\DosDevices**目录的多个版本。 请确保您的驱动程序在您想要的版本中创建其符号链接。 有关详细信息，请参阅[本地和全局 MS-DOS 设备名称](local-and-global-ms-dos-device-names.md)。

若要从用户模式访问**DosDevices**命名空间，请在打开文件名时指定 **\\\\\\。** 可以通过调用**CreateFile （）** 在用户模式下打开相应的设备。

例如，下面的代码示例在用户模式下打开 \\\\DosDevices\\\\*DosDeviceName*设备。

```cpp
file = CreateFileW(L"\\\\.\\DosDeviceName",
  GENERIC READ | GENERIC WRITE,
    0,
    NULL,
    OPEN_EXISTING,
    0,
    NULL);
```

还可以通过使用用户模式**DefineDosDevice**例程从用户模式应用程序创建符号链接。 有关详细信息，请参阅 Microsoft Windows SDK。

 

 




