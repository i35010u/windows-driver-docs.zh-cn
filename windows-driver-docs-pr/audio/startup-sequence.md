---
title: 启动顺序
description: 启动顺序
ms.assetid: bf88b9de-f4c4-4f9c-9355-603789b9ad3d
keywords:
- 适配器驱动程序 WDK 音频，启动序列
- 启动序列 WDK 音频
- 音频适配器 WDK，启动序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 747575cef67dd5d2028cee59acec3b1641433a4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354278"
---
# <a name="startup-sequence"></a>启动顺序


## <span id="startup_sequence"></span><span id="STARTUP_SEQUENCE"></span>


由于适配器驱动程序安装为一个内核模式驱动程序服务中，操作系统在系统启动时加载适配器驱动程序，并调用驱动程序的[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 **DriverEntry**例程接收两个参数： 驱动程序对象和注册表路径名称。 **DriverEntry**应调用 PortCls 函数[ **PcInitializeAdapterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver)与驱动程序对象和注册表路径名称参数以及第三个参数，这是指向的指针适配器驱动程序[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)函数。

在以下示例中，该驱动程序的[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数将传递函数指针`MyAddDevice`，它指向的驱动程序[ **AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)函数，作为第三个参数[ **PcInitializeAdapterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver)例程。

```cpp
NTSTATUS 
  DriverEntry( 
    PDRIVER_OBJECT  DriverObject,
    PUNICODE_STRING  RegistryPath
    )
  {
      return PcInitializeAdapterDriver(DriverObject, RegistryPath, MyAddDevice);
  }
```

[ **PcInitializeAdapterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver)例程安装提供[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程在驱动程序对象的驱动程序扩展和安装驱动程序中的 PortCls 驱动程序的 IRP 处理程序对象本身。

下面的代码是在驱动程序的示例实现`MyAddDevice`函数。

```cpp
#define MAX_MINIPORTS 6    // maximum number of miniports
NTSTATUS
  MyAddDevice(
    PDRIVER_OBJECT  DriverObject,
    PDEVICE_OBJECT  PhysicalDeviceObject 
    )
  {
      return PcAddAdapterDevice(DriverObject, PhysicalDeviceObject, MyStartDevice,
                                MAX_MINIPORTS, 0);
  }
```

此函数将调用 PortCls 函数**PcAddAdapterDevice**并将其与*物理设备对象 (PDO)* 系统提供。 新 FDO 创建扩展名为 PortCls 用来存储有关设备的上下文信息。 此上下文会包含`MyStartDevice`提供的函数指针`MyAddDevice`。

操作系统确定哪些资源 （中断、 DMA 通道、 I/O 端口地址等） 要将分配到设备后，将发送设备启动的请求 ([**IRP\_MN\_开始\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 在对此请求的响应，PortCls 驱动程序中的请求处理程序调用适配器驱动程序的`MyStartDevice`函数，在下面的示例代码所示：

```cpp
NTSTATUS
  MyStartDevice(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PRESOURCELIST ResourceList
    )
  {
    ...
  }
```

请求处理程序提供`MyStartDevice`带有指针指向的设备对象，IRP\_MN\_启动\_设备请求和资源的列表 (请参阅[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iresourcelist))。 `MyStartDevice`函数分区到所需的每个需要启动的微型端口驱动程序的资源的资源的列表。 该函数然后启动每个微型端口驱动程序，并将控制权返回给 PortCls，完成 IRP，并将控制权返回给操作系统。

驱动程序启动代码的更多示例，请参阅 Microsoft Windows Driver Kit (WDK) 中的示例音频适配器驱动程序。

 

 




