---
title: 虚拟子单元驱动程序说明
description: 虚拟子单元驱动程序说明
ms.assetid: e484f815-73a8-46f1-956e-ee16b1856bd0
keywords:
- Avc 函数驱动程序 WDK，虚拟子单位驱动程序
- 虚拟子单位驱动程序 WDK AV/C
- 外部设备 WDK AV/C
- IOCTL_AVC_CLASS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca049d36082fae78fa7ef090595053b578446caf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845280"
---
# <a name="virtual-subunit-driver-notes"></a>虚拟子单元驱动程序说明


虚拟子源驱动程序通过使用具有*AVC*的[**IOCTL\_AVC\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)接口，响应来自外部 AV/c 设备的控制、状态和通知 AV/c 请求和命令。

IOCTL\_AVC\_类 subfunction 代码[**AVC\_函数\_获取\_请求**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)和[**AVC\_函数\_发送\_响应**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-send-response)是虚拟子单位驱动程序的关键机制与虚拟驱动程序堆栈的其余部分交互。 虚拟子单位驱动程序提交**AVC\_函数\_** 在其 IRP\_MN 中获取\_请求 Irp 到*AVC* [ **\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)例程（IRP\_MN\_启动\_设备已由堆栈中的基础驱动程序完成。 每次收到虚拟子单位的请求时，都将调用**AVC\_函数\_获取\_请求**IRP 的 i/o 完成例程。 I/o 完成例程必须发送响应（通过**AVC\_函数\_通过异步 IRP 发送\_响应**）在 100 ms 内（根据 AV/C 协议规则）;它可以使用请求中包含的[**AVC\_命令\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)结构来发送响应。 然后，它必须重新提交**AVC\_函数，\_获取\_请求**IRP，然后最后从响应的 i/o 完成例程返回。

虚拟驱动程序堆栈中的子单元驱动程序无法直接将命令发送到外部设备。 对等驱动程序堆栈提供此功能。 不过，虚拟子单位驱动程序可以使用[**AVC\_函数\_FIND\_对等\_do**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-find-peer-do) and [**AVC\_函数\_对等\_执行**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-peer-do-list) [**IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)的 subfunctions\_LIST，以发现和引用*AVC*的对等实例，然后与外部 AV/C 子单元连接交互。\_\_

对于枚举的每个虚拟子单位， *Avc*会创建相应的设备对象。 因此，在添加和删除虚拟子单位后， *Avc*会触发 IEEE 1394 总线重置。 此重置允许 IEEE 1394 总线上的其他设备检测正在计算机上公开的新功能。 虚拟子单位驱动程序基于*Avc*实例的注册表设置进行加载，并且可在运行时通过 IOCTL 代码请求进行添加和删除。 请注意， *Avc*不能区分同一类型的多个虚拟子单元连接，因此添加和删除这些子单元连接将加载并卸载具有最高子单位标识符的相应虚拟子驱动器驱动程序。

虚拟子单位驱动程序可以是厚或精简。 唯一的要求是将其编写为 WDM 驱动程序。 厚驱动程序实现了虚拟设备的大多数（如果不是全部）功能。 瘦驱动程序提供了虚拟设备功能的代理接口，可以是其他驱动程序或用户模式组件。 用户模式与虚拟子单位驱动程序之间的接口是特定于实现的，并且可以通过 IOCTL 代码、专用设备接口（请参阅[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)）或[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) （WMI）来实现。

即使\_ 和 MOD\_ 值与 INF 文件中指定的值相同，后者导致*61883*的虚拟实例加载。 当*Avc*枚举虚拟子单位时，可以指定 TYP\_ 和 ID\_ 值。

虚拟子单位的枚举通过使用[**IOCTL\_AVC 来完成：\_更新\_虚拟\_子虚拟**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)\_[**信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)和[**IOCTL\_AVC\_总线\_重置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)IOCTL 代码。\_\_\_\_\_

有必要发送正确的 IEEE 1394 IOCTLs、 **IEEE1394\_api\_添加\_虚拟\_设备**和**IEEE1394\_api\_删除\_虚拟\_设备**以开始枚举过程。 有关详细信息（IOCTL 的子命令\_IEEE1394\_API\_请求）。 *61883*文件已包含用于此目的的设备标识符（ID）： V1394\\A02D & 10001，但自定义 inf 文件中可能会提供不同的标识符。

可以通过使用 INF 文件来静态枚举虚拟子单位的替代方法。

虚拟设备列表键下的每个值都是一个打包的子地址（子类型和最大标识符组合在一起，如 AV/C 常规规范中所述）。 与子单位地址相关联的名称并不重要，但它对于该实例必须是唯一的。 以编程方式创建时，将为值名称提供序列号以避免冲突。

例如，若要通过 INF 文件创建单个虚拟调谐器子单位，请使用以下**AddReg**指令：

```INF
[Subunit_Device.NT.HW.AddReg]
HKR,%VirtualAvc.DeviceList%,Tuner,0x00000001,0x28 ;0x00000001 = Binary value, 0x28 = Registry key value
```

此指令将 REG\_二进制值的0x28 （子类型0x5 打包到最重要的5位，并将最大的0x0 标识符打包到最不重要的三位）。 此处的最大标识符为0x0，表示将有该类型的单个子单位。

**请注意**  ：还必须在子区域的 INF 文件的 `[Strings]` 部分中定义 `%VirtualAvc.DeviceList%` 令牌。
