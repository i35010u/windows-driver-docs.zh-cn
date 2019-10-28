---
title: 处理存储类驱动程序中的 PnP 启动
description: 处理存储类驱动程序中的 PnP 启动
ms.assetid: 8d4ccd09-c5d2-4c9b-b94d-e22c916f0043
keywords:
- 存储类驱动程序 WDK、PnP
- 类驱动程序 WDK 存储，PnP
- PnP WDK 存储
- 即插即用 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c86bab639bba90c3ba0f7cb0d0876d935f14d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837556"
---
# <a name="handling-pnp-start-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 启动


## <span id="ddk_handling_pnp_start_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序在 PnP 管理器使用启动请求（IRP\_MJ\_PNP 和[**irp\_MN\_start\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)）调用类驱动程序的[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程时执行特定于设备的初始化。 存储类驱动程序的*DispatchPnP*例程要么调用内部*StartDevice*例程，要么实现同一功能内联。 因为发送到 FDO 的启动请求必须首先由堆栈中的最低驱动程序处理，所以存储类驱动程序的*DispatchPnP*例程会将请求转发到带有[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的下一个较低版本的驱动程序，然后再调用*StartDevice*。 如果请求已发送到 PDO，则驱动程序在处理请求之前，不需要转发该请求。

存储类驱动程序的内部*StartDevice*例程使用驱动程序确定的数据设置其 FDO 的设备扩展，以管理设备的 i/o 请求。 有关详细信息，请参阅[设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

*StartDevice*例程应启用驱动程序在其*AddDevice*例程中注册的任何设备接口。 （请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。）它还可以为其设备对象创建一个符号链接。

在较低的设备启动完成后，驱动程序可能会假设设备处于 D0 电源状态（完全打开和操作）。 如果设备未完全启动，端口驱动程序将排队请求，直到设备准备就绪。 但是，如果驱动程序的*StartDevice*例程需要执行需要浪涌电流的任何操作（例如，加速磁盘驱动器），则在执行该操作之前，驱动程序必须将 D0 电源请求发送到下一个较低的驱动程序。

类型为 FILE\_设备的设备的驱动程序\_磁盘或文件\_设备\_大容量\_存储可以注册空闲检测，并通过指定保留和性能来使用设备类的标准电源策略超时**PoRegisterDeviceforIdleDetection**调用中的超时值-1。

有关存储类驱动程序的*DispatchPnP*例程的详细信息，请参阅[处理存储外围设备的 PnP 请求](handling-pnp-requests-to-storage-peripherals.md)。 有关处理 PnP 启动请求的详细信息，请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)。

 

 




