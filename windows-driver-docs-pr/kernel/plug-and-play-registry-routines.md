---
title: 即插即用注册表例程
description: 即插即用注册表例程
ms.assetid: d526af4e-8b33-46fb-9af9-b0d9b9f1913a
keywords:
- 注册表 WDK 内核插
- 驱动程序注册表信息 WDK 内核插
- 插 WDK 内核，注册表例程
- 硬件密钥 WDK 内核
- 软件密钥 WDK 内核
- IoOpenDeviceRegistryKey
- IoOpenDeviceInterfaceRegistryKey
- 即插即用 WDK 内核，注册表例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffa464523400ac527775ae1a350c74a45749e4cb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350388"
---
# <a name="plug-and-play-registry-routines"></a>即插即用注册表例程


插管理器将某些注册表项与驱动程序、 其设备和其设备接口实例相关联。 驱动程序可以使用这些密钥来存储与该驱动程序，或特定的设备或设备接口实例关联的持久性属性。

驱动程序必须永远不会直接访问这些密钥。 Windows 的未来版本可能会将存储在不同位置的信息在注册表中，或在注册表外完全。 驱动程序必须直接访问以下树中的任何键：

-   HKLM\\SYSTEM\\CurrentControlSet\\Control\\Class

-   HKLM\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses

-   HKLM\\SYSTEM\\CurrentControlSet\\Enum

-   HKLM\\系统\\CurrentControlSet\\硬件配置文件

相反，驱动程序使用[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)并[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)例程来访问其即插即用键。

PnP 管理器将分配一个密钥用于驱动程序，称为驱动程序的软件密钥，并将每个设备，称为设备的硬件密钥的密钥。 **IoOpenDeviceRegistryKey**例程可用于打开这两个密钥。 值*DevInstKeyType*参数确定要打开哪个密钥。 指定 PLUGPLAY\_REGKEY\_驱动程序以打开软件密钥或 PLUGPLAY\_REGKEY\_到硬件密钥的设备。 *DeviceObject*参数指定的设备或驱动程序。 (该驱动程序还可以访问其硬件和软件的密钥，相对于当前的硬件配置文件，通过运算 PLUGPLAY\_REGKEY\_当前\_到 HWPROFILE *DevInstKeyType*。)

**IoOpenDeviceInterfaceRegistryKey**打开与特定设备接口实例相关联的密钥。 实例由其名称，即[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)返回[ **IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)，[ **IoGetDeviceInterfaceAlias**](https://msdn.microsoft.com/library/windows/hardware/ff549180)，或[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)。 将字符串作为传递*SymbolicLinkValue*参数**IoOpenDeviceInterfaceRegistryKey**。

在一个 INF 文件，或通过使用，还可以设置这些密钥**SetupDi * Xxx*** 例程。 有关详细信息，请参阅[驱动程序的注册表项](https://msdn.microsoft.com/library/windows/hardware/ff549538)。

这两[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)并[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)打开密钥句柄，提供访问权限通过指定*DesiredAccess*参数。 驱动程序随后使用**Zw * Xxx*** 注册表例程，如[ **ZwQueryValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567069)并[ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)进行访问和操作键。 该驱动程序不能再使用该句柄后，该驱动程序通过调用关闭句柄[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。 有关详细信息，请参阅[使用注册表项对象的句柄](using-a-handle-to-a-registry-key-object.md)。

下面的代码示例演示了如何使用**IoOpenDeviceRegistryKey**并**ZwSetValueKey**设置与设备的硬件密钥下名为"Value"的值关联的数据。

```cpp
PDEVICE_OBJECT pDeviceObject; // A pointer to the PDO for the device.
HANDLE handle;
UNICODE_STRING ValueName;
ULONG Value = 109; // This is the value we're setting the key to.
NTSTATUS status;

RtlInitUnicodeString(&ValueName, L"Value");

status = IoOpenDeviceRegistryKey(pDeviceObject, PLUGPLAY_REGKEY_DEVICE, KEY_READ, &handle);

if (NTSUCCESS(status)) {
  status = ZwSetValueKey(handle, ValueName, 0, REG_DWORD, &Value, sizeof(ULONG));
  if (NTSUCCESS(status) {
    ZwClose(handle);
  } else {
    // Handle error.
  }
  // Handle error.
}
```

请注意，对注册表项的访问可能受限，因此调用[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)并[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)应指定所需的最低权限*DesiredAccess*。 如果该驱动程序请求的访问权限，不允许，任一例程将返回状态\_访问\_被拒绝。 具体而言，驱动程序不应指定密钥\_所有\_访问。

 

 




