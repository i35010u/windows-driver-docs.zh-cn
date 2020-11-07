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
ms.openlocfilehash: 566f619b1e3fb21bd83d0d7ee377ab7071f9de82
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361301"
---
# <a name="startup-sequence"></a>启动顺序


## <span id="startup_sequence"></span><span id="STARTUP_SEQUENCE"></span>


由于适配器驱动程序作为内核模式驱动程序服务安装，因此操作系统将在系统启动时加载适配器驱动程序，并调用驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 **DriverEntry** 例程接收两个参数：驱动程序对象和注册表路径名称。 **DriverEntry** 应使用驱动程序对象和注册表路径名称参数加上第三个参数（指向适配器驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)函数的指针）来调用 PortCls 函数 [**PcInitializeAdapterDriver**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver) 。

在下面的示例中，驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数将 `MyAddDevice` 指向驱动程序的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 函数的函数指针传递为 [**PcInitializeAdapterDriver**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver) 例程的第三个参数。

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

[**PcInitializeAdapterDriver**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)例程在驱动程序对象的驱动程序扩展中安装提供的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，并在驱动程序对象本身中安装 PORTCLS 驱动程序的 IRP 处理程序。

下面的代码是驱动程序函数的示例实现 `MyAddDevice` 。

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

此函数将调用 PortCls 函数 [**PcAddAdapterDevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)，该函数将创建指定的适配器设备，将驱动程序与设备关联，并存储一个指向适配器驱动程序函数的指针，该指针在 `MyStartDevice` 操作系统启动设备时调用 (请参阅 [启动设备](../kernel/starting-a-device.md)) 。 **PcAddAdapterDevice** 例程 *(FDO) 创建一个功能设备对象* ，并将其与系统提供 *(PDO) 的物理设备对象* 相关联。 将创建新的 FDO，其中包含 PortCls 用于存储有关设备的上下文信息的扩展。 此上下文包括 `MyStartDevice` 由提供的函数指针 `MyAddDevice` 。

操作系统确定哪些资源 (中断、DMA 通道、i/o 端口地址等) 分配给设备后，它会向设备发送请求， ( [**IRP \_ MN \_ start \_ device**](../kernel/irp-mn-start-device.md)) 。 为响应此请求，PortCls 驱动程序中的请求处理程序将调用适配器驱动程序的 `MyStartDevice` 函数，如下面的示例代码所示：

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

请求处理程序提供 `MyStartDevice` 了指向设备对象、IRP \_ MN \_ 开始 \_ 设备请求和资源列表 (的指针，请参阅 [IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)) 。 `MyStartDevice`函数将资源列表分区为每个需要启动的微型端口驱动程序所需的资源。 然后，该函数启动每个微型端口驱动程序并将控制返回到 PortCls，这将完成 IRP 并将控制返回给操作系统。

有关驱动程序启动代码的更多示例，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的示例音频适配器驱动程序。

