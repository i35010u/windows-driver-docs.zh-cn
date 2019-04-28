---
title: 命名的设备对象
description: 命名的设备对象
ms.assetid: 4e24f0c1-57b2-4e06-a7f5-9a93d365ac8c
keywords:
- 设备对象 WDK 内核，名为
- 指定的设备对象 WDK 内核
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bb7c6f5ce76485b5715fb5b5a9a7c8de02ca4b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341957"
---
# <a name="named-device-objects"></a>命名的设备对象





可以命名或未命名的设备对象，如所有对象管理器对象。 在用户模式应用程序发出的 I/O 请求，它按名称指定操作的目标。 对象管理器可解析名称来确定 I/O 请求的目标。

> [!IMPORTANT]
> 若要帮助增加驱动程序安全名称设备对象仅在必要时。 指定的设备对象通常只是必要由于历史原因，例如如果你希望打开使用特定名称的设备的应用程序，或在使用非 PNP 设备/控制的设备。  请注意，WDF 驱动程序不需要命名它们即插即用设备以便创建符号链接使用[WdfDeviceCreateSymbolicLink](https://msdn.microsoft.com/library/windows/hardware/ff545939.aspx)。

调用时，驱动程序可以指定一个设备对象的名称[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)或[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)来创建的设备对象。 有关何时以及如何命名的设备对象的详细信息，请参阅[NT 设备名称](nt-device-names.md)。
  
指定的设备对象还具有 MS-DOS 设备名称，即符号链接创建由[ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)或[ **IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050). WDM 驱动程序通常不需要 MS-DOS 设备名称。 有关详细信息，请参阅[MS-DOS 设备名称](ms-dos-device-names.md)。

> [!IMPORTANT]
> 如果您使用指定的设备对象则可以使用[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)并指定 SDDL 以确保其安全。 当您实现[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)始终为 DeviceClassGuid 指定自定义类 GUID。 不应指定一个现有的类 GUID 此处。 这样做有可能会破坏安全设置或其他设备属于该类的兼容性。 有关详细信息，请参阅[WdmlibIoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/mt800803.aspx)。
> 
> 若要允许应用程序或其他 WDF 驱动程序来访问你的即插即用设备，则应使用设备接口。 有关详细信息，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)。 设备接口可作为设备堆栈的 PDO 的符号链接。 一旦方法控制对 PDO 的访问是通过在你 INF 中指定的 SDDL 字符串。 如果的 SDDL 字符串不是 INF 文件中，Windows 将应用的默认安全描述符。 有关详细信息，请参阅[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)并[设备对象的 SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)。


本部分包含以下小节：

[NT 设备名称](nt-device-names.md)

[MS-DOS 设备名称](ms-dos-device-names.md)

 

 




