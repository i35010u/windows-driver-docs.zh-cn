---
title: 驱动程序包隔离
ms.date: 10/01/2019
ms.openlocfilehash: 7c6c8824e143ffa893d79977bdd424263939ca16
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706982"
---
# <a name="driver-package-isolation"></a>驱动程序包隔离

驱动程序包隔离介绍了一组最佳做法，使驱动程序更能适应外部更改、更易于更新以及更易于安装。

下表左列显示的是不再推荐的旧驱动程序做法，右列是推荐的最佳做法。

|非隔离驱动程序|独立驱动程序|
|-|-|
|INF 将文件复制到 System32\drivers|驱动程序文件从驱动程序存储运行|
|使用硬编码路径与其他驱动程序交互|使用系统提供的功能或设备接口与其他驱动程序交互|
|将路径硬编码到全局注册表位置|使用 HKR 和系统提供的功能获取注册表和文件状态的相对位置|
|运行时文件写入任何位置|驱动程序将文件写入系统提供的位置|


## <a name="run-from-driver-store"></a>从驱动程序存储运行

所有独立驱动程序包都将其驱动程序包文件保留在驱动程序存储中。 这意味着，它们在其 INF 中指定 [DIRID 13](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) 以在安装时指定驱动程序包文件的位置  。

WDM 或 KMDF 驱动程序从 DriverStore 中运行并需要从其驱动程序包访问其他文件，它可以使用 [IoQueryFullDriverPath](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioqueryfulldriverpath) 来查找它的路径、获取加载它的目录路径以及查找与该路径相关的配置文件  。

或者，在 Windows 10 版本 1803 及更高版本中，使用 DriverDirectoryImage 作为目录类型来调用 [IoGetDriverDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory)，以获取加载该驱动程序的目录路径   。

对于 INF 负载的文件，INF 中该文件的 [SourceDisksFiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) 条目中列出的 subdir 必须与 INF 中该文件的 [DestinationDirs](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section) 条目中列出的 subdir 匹配    。

此外，[CopyFiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive) 指令不能用于重命名文件  。 这些限制是必需的，这样在设备上安装 INF 才不会导致在 DriverStore 目录中创建新文件。

由于 [SourceDisksFiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) 条目无法具有多个文件名相同的条目，并且 CopyFiles 不能用于重命名文件，因此 INF 引用的每个文件必须具有唯一的文件名  。

有关从驱动程序存储查找和加载文件的详细信息，请参阅[通用驱动程序方案](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios#dynamically-finding-and-loading-files-from-the-driver-store)。

## <a name="using-device-interfaces"></a>使用设备接口

需要在驱动程序之间共享状态时，应该只有一个驱动程序拥有共享状态，并且该驱动程序应该为其他驱动程序提供一种读取和修改该状态的方法   。

通常，拥有该状态的驱动程序会在自定义设备接口类中公开一个设备接口。 当驱动程序准备好让其他驱动程序访问该状态时，它将启用该接口。 其他驱动程序可以注册[设备接口到达通知](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)。 要访问状态，自定义设备接口类可以定义两个协议之一：

* I/O 协议，可以与提供访问状态的机制的设备接口类相关联  。 其他驱动程序使用已启用的设备接口来发送符合协议的 I/O 请求。
* 直接调用接口通过查询接口返回  。 其他驱动程序可以通过发送 [IRP_MN_QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) 从驱动程序检索函数指针以进行调用。

或者，如果拥有该状态的驱动程序允许直接访问该状态，其他驱动程序则可以通过使用系统提供的功能以编程方式访问设备接口状态来访问该状态。

这些接口或状态（取决于使用的共享方法）需要进行正确的版本控制，以便拥有该状态的驱动程序可以独立于访问该状态的其他驱动程序而获得服务。 驱动程序供应商不能同时依赖于正在获得服务且版本相同的两个驱动程序。  

因为控制接口的设备和驱动程序变化不定，所以驱动程序和应用程序应该避免在组件启动时调用 [IoGetDeviceInterfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来获取已启用接口的列表  。

最佳做法是注册设备接口到达或删除的通知，然后调用适当的函数来获取计算机上现有的已启用接口的列表。

有关设备接口的详细信息，请参阅：

* [使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)
* [注册获取设备接口到达和设备删除通知](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)
* [注册设备接口更改通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)

## <a name="reading-and-writing-state"></a>读取和写入状态

> [!NOTE]
> 如果组件使用的是设备或设备接口属性来存储状态，则继续使用该方法和适当的 OS API 来存储并访问状态  。 以下指南适用于需要由组件存储的其他状态  。

对各种状态的访问应该通过调用函数来完成，这些函数向调用方提供状态的位置，然后系统将读取/写入与该位置相关的状态。 请勿使用硬编码的绝对注册表路径和文件路径。

本节包含以下小节：

* [PnP 设备注册表状态](#pnp-device-registry-state)
* [设备接口注册表状态](#device-interface-registry-state)
* [服务注册表状态](#service-registry-state)
* [设备文件状态](#device-file-state)
* [服务文件状态](#service-file-state)

### <a name="pnp-device-registry-state"></a>PnP 设备注册表状态

独立驱动程序包和用户模式组件通常使用两个位置在注册表中存储设备状态。 它们是用于设备的硬件密钥（设备密钥）和用于设备的软件密钥（驱动程序密钥）   。 若要检索这些注册表位置的句柄，请根据使用的平台使用以下选项之一：

* [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) (WDM)
* [**WdfDeviceOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)、[**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) (WDF)
* [**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)（用户模式代码）
* [**INF AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) 指令，使用引用自 [INF DDInstall](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section) 部分或 [DDInstall.HW](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section) 部分的 add-registry-section 中的 HKR reg-root 条目，如下所示  ：

```
[ExampleDDInstall.HW]
AddReg = Example_DDInstall.AddReg

[Example_DDInstall.AddReg] 
HKR,,ExampleValue,,%13%\ExampleFile.dll
```
### <a name="device-interface-registry-state"></a>设备接口注册表状态

使用设备接口与其他驱动程序和组件共享状态。 请勿将路径硬编码到全局注册表位置。

若要读取和写入设备接口注册表状态，请根据使用的平台使用以下选项之一：

* [**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) (WDM)
* [**CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)（用户模式代码）
* [INF AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) 指令，使用引用自 [add-interface-section](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive) 部分的 add-registry-section 中的 HKR reg-root 条目  

### <a name="service-registry-state"></a>服务注册表状态

INF 为驱动程序和 Win32 服务设置的注册表值应存储在服务的“参数”子项下，方法是在 [AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) 部分中提供 HKR 行，然后在 INF 的服务安装部分引用该部分。  例如：

```
[ExampleDDInstall.Services]
Addservice = ExampleService, 0x2, Example_Service_Inst

[Example_Service_Inst]
DisplayName    = %ExampleService.SvcDesc%
ServiceType    = 1
StartType      = 3
ErrorControl   = 1
ServiceBinary  = %13%\ExampleService.sys
AddReg=Example_Service_Inst.AddReg

[Example_Service_Inst.AddReg]
HKR, Parameters, ExampleValue, 0x00010001, 1
```

若要访问该状态的位置，请根据平台使用下列函数之一：

* [**IoOpenDriverRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendriverregistrykey) (WDM)
* [**WdfDriverOpenParametersRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey) (WDF)
* **GetServiceRegistryStateKey**（Win32 服务）

### <a name="device-file-state"></a>设备文件状态

如果需要写入与设备相关的文件，这些文件应相对于通过 OS API 提供的句柄或文件路径进行存储。 例如，特定于该设备的配置文件就是一个应存储在此处的文件类型。

* [**IoGetDeviceDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicedirectory) (WDM)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring) (WDF)

### <a name="service-file-state"></a>服务文件状态

Win32 和驱动程序服务均读取和写入关于本身的状态。

若要访问服务自己的内部状态值，该服务需使用下列选项之一： 

* [**IoGetDriverDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory)（WDM 和 KMDF）
* [**WdfDriverRetrieveDriverDataDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) (UMDF)
* **GetServiceDirectory**（Win32 服务）

若要与其他组件共享服务的内部状态，请使用受控制的、受版本控制的接口，而不是直接注册表或文件读取。

## <a name="driverdata-and-programdata"></a>DriverData 和 ProgramData

用作可与其他组件共享的中间操作的一部分的文件应该写入 DriverData 或 ProgramData 位置   。

这些位置为组件提供一个位置，用于写入临时状态或旨在由其他组件使用、可能从某一系统收集和复制以供另一系统处理的状态。  例如，自定义日志文件或故障转储符合此描述。

### <a name="driverdata"></a>DriverData

`DriverData` 目录在 Windows 10 版本 1803 及更高版本中可用。 此目录可由用户模式和内核模式组件通过不同机制进行访问。

内核模式驱动程序应使用系统提供的名为 `\DriverData` 的符号链接访问 `DriverData` 目录。
用户模式程序应使用环境变量 `%DriverData%` 访问 `DriverData` 目录。

### <a name="programdata"></a>ProgramData

`%ProgramData%` 用户模式环境变量适用于存储数据时要使用的用户模式组件。 

避免在 `DriverData` 或 `ProgramData` 目录的根目录中写入文件。 请改用公司名称创建子目录，然后在在该目录中写入文件和更多子目录。

例如，对于 Contoso 的公司名称，内核模式驱动程序可将自定义日志写入 `\DriverData\Contoso\Logs`，用户模式应用程序可收集或分析 `%DriverData%\Contoso\Logs` 中的日志文件。

