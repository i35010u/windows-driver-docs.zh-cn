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
ms.openlocfilehash: eb1c2b8cfd1b661b475b3a198a4d7da1ac22b2fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830121"
---
# <a name="startup-sequence"></a>启动顺序


## <span id="startup_sequence"></span><span id="STARTUP_SEQUENCE"></span>


由于适配器驱动程序作为内核模式驱动程序服务安装，因此操作系统将在系统启动时加载适配器驱动程序，并调用驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程。 **DriverEntry**例程接收两个参数：驱动程序对象和注册表路径名称。 **DriverEntry**应使用驱动程序对象和注册表路径名称参数加上第三个参数（指向适配器驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)函数的指针）来调用 PortCls 函数[**PcInitializeAdapterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver) 。

在下面的示例中，驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数将函数指针 `MyAddDevice`（指向驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)函数）传递给[**PcInitializeAdapterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)例程的第三个参数。

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

[**PcInitializeAdapterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)例程在驱动程序对象的驱动程序扩展中安装提供的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，并在驱动程序对象本身中安装 PORTCLS 驱动程序的 IRP 处理程序。

下面的代码是驱动程序的 `MyAddDevice` 函数的示例实现。

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

此函数将调用 PortCls 函数**PcAddAdapterDevice** ，并将其与系统提供的*物理设备对象（PDO）* 相关联。 将创建新的 FDO，其中包含 PortCls 用于存储有关设备的上下文信息的扩展。 此上下文包括 `MyAddDevice`提供的 `MyStartDevice` 函数指针。

操作系统确定要分配给设备的资源（中断、DMA 通道、i/o 端口地址等）后，它会向设备发送请求以启动（[**IRP\_MN\_start\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)）。 为响应此请求，PortCls 驱动程序中的请求处理程序将调用适配器驱动程序的 `MyStartDevice` 函数，如下面的示例代码所示：

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

请求处理程序提供 `MyStartDevice` 指针指向设备对象、IRP\_MN\_开始\_设备请求和资源列表（请参阅[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)）。 `MyStartDevice` 函数将资源列表分区为每个需要启动的微型端口驱动程序所需的资源。 然后，该函数启动每个微型端口驱动程序并将控制返回到 PortCls，这将完成 IRP 并将控制返回给操作系统。

有关驱动程序启动代码的更多示例，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的示例音频适配器驱动程序。

 

 




