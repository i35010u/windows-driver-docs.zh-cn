---
title: 处理存储类驱动程序中的 PnP 启动
description: 处理存储类驱动程序中的 PnP 启动
keywords:
- 存储类驱动程序 WDK、PnP
- 类驱动程序 WDK 存储，PnP
- PnP WDK 存储
- 即插即用 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bf251e2f40c70bcd54637b6015e459bbbe3403d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804531"
---
# <a name="handling-pnp-start-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 启动


## <span id="ddk_handling_pnp_start_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序在 PnP 管理器使用启动请求调用类驱动程序的 [**DispatchPnP**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程时执行特定于设备的初始化， (irp \_ MJ \_ PnP with [**irp \_ MN \_ start \_ device**](../kernel/irp-mn-start-device.md)) 。 存储类驱动程序的 *DispatchPnP* 例程要么调用内部 *StartDevice* 例程，要么实现同一功能内联。 因为发送到 FDO 的启动请求必须首先由堆栈中的最低驱动程序处理，所以存储类驱动程序的 *DispatchPnP* 例程会将请求转发到带有 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的下一个较低版本的驱动程序，然后再调用 *StartDevice*。 如果请求已发送到 PDO，则驱动程序在处理请求之前，不需要转发该请求。

存储类驱动程序的内部 *StartDevice* 例程使用驱动程序确定的数据设置其 FDO 的设备扩展，以管理设备的 i/o 请求。 有关详细信息，请参阅 [设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

*StartDevice* 例程应启用驱动程序在其 *AddDevice* 例程中注册的任何设备接口。  (参阅 [设备接口类](../install/overview-of-device-interface-classes.md)。 ) 它也可能为其设备对象创建符号链接。

在较低的设备启动完成后，驱动程序可能会假设设备处于 D0 电源状态 (完全打开且可正常运行) 。 如果设备未完全启动，端口驱动程序将排队请求，直到设备准备就绪。 但是，如果驱动程序的 *StartDevice* 例程需要执行需要浪涌电流的任何操作（例如，加速磁盘驱动器），则在执行该操作之前，驱动程序必须将 D0 电源请求发送到下一个较低的驱动程序。

类型为 "文件 \_ 设备磁盘" 或 " \_ 文件 \_ 设备大容量存储" 的设备的驱动程序 \_ \_ 可以通过在其 **PoRegisterDeviceforIdleDetection** 调用中指定保留和性能超时值-1 来注册空闲检测并使用设备类的标准电源策略超时值。

有关存储类驱动程序的 *DispatchPnP* 例程的详细信息，请参阅 [处理存储外围设备的 PnP 请求](handling-pnp-requests-to-storage-peripherals.md)。 有关处理 PnP 启动请求的详细信息，请参阅 [启动设备](../kernel/starting-a-device.md)。

 

