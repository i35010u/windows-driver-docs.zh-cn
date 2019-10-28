---
title: 即插即用注册表例程
description: 即插即用注册表例程
ms.assetid: d526af4e-8b33-46fb-9af9-b0d9b9f1913a
keywords:
- 注册表 WDK 内核，即插即用
- 驱动程序注册表信息 WDK 内核，即插即用
- 即插即用 WDK 内核，注册表例程
- 硬件密钥 WDK 内核
- 软件密钥 WDK 内核
- IoOpenDeviceRegistryKey
- IoOpenDeviceInterfaceRegistryKey
- PnP WDK 内核，注册表例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09dc6832584e456d6516a7dd3d884f410fc1ae60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838512"
---
# <a name="plug-and-play-registry-routines"></a>即插即用注册表例程


即插即用管理器将某些注册表项与驱动程序、其设备及其设备接口实例相关联。 驱动程序可以使用这些密钥来存储与驱动程序相关联的持久性属性，或使用特定设备或设备接口实例。

驱动程序决不能直接访问这些密钥。 将来版本的 Windows 可以将信息存储在注册表中的不同位置，或者存储在注册表外部。 驱动程序不能直接访问以下树中的任何密钥：

-   HKLM\\SYSTEM\\CurrentControlSet\\控件\\类

-   HKLM\\SYSTEM\\CurrentControlSet\\控件\\DeviceClasses

-   HKLM\\SYSTEM\\CurrentControlSet\\枚举

-   HKLM\\SYSTEM\\CurrentControlSet\\硬件配置文件

相反，驱动程序将使用[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)和[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)例程来访问其 PnP 密钥。

PnP 管理器为驱动程序分配一个密钥（称为驱动程序的软件密钥），并为每个设备分配一个密钥，称为设备的硬件密钥。 **IoOpenDeviceRegistryKey**例程可用于打开任意一个密钥。 *DevInstKeyType*参数的值确定要打开的键。 指定 PLUGPLAY\_REGKEY\_驱动程序以打开软件密钥，或 PLUGPLAY\_REGKEY\_设备注册到硬件密钥。 *DeviceObject*参数指定设备或驱动程序。 （驱动程序还可以通过 ANDing PLUGPLAY\_REGKEY\_当前\_HWPROFILE 中到*DevInstKeyType*，来访问其硬件和软件密钥，方法是使用当前硬件配置文件。）

**IoOpenDeviceInterfaceRegistryKey**打开与特定设备接口实例相关联的密钥。 实例由其名称标识，该名称是[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)、 [**IoGetDeviceInterfaceAlias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacealias)或[**IOREGISTERDEVICEINTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)返回的[**UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)。 字符串作为*SymbolicLinkValue*参数传递给**IoOpenDeviceInterfaceRegistryKey**。

还可以在 INF 文件中或使用**SetupDi * Xxx*** 例程来设置这些密钥。 有关详细信息，请参阅[驱动程序的注册表项](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)。

[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)和[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)都提供打开的密钥句柄，其中包含*DesiredAccess*参数指定的访问权限。 然后，该驱动程序使用**Zw * Xxx*** 注册表例程（如[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)和[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)）访问和操作该密钥。 当驱动程序不再使用该句柄之后，驱动程序将通过调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来关闭该句柄。 有关详细信息，请参阅[使用注册表项对象的句柄](using-a-handle-to-a-registry-key-object.md)。

下面的代码示例演示了如何使用**IoOpenDeviceRegistryKey**和**ZwSetValueKey**来设置与设备硬件密钥下名为 "value" 的值相关联的数据。

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

请注意，可以限制对注册表项的访问，因此，对[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)和[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)的调用应指定*DesiredAccess*所需的最小权限。 如果驱动程序请求不允许的访问权限，则常规返回状态\_访问\_拒绝。 具体而言，驱动程序不应\_所有\_访问中指定密钥。

 

 




