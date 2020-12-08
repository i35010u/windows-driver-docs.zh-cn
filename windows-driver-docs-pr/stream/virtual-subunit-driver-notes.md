---
title: 虚拟子单元驱动程序说明
description: 虚拟子单元驱动程序说明
keywords:
- Avc.sys 函数驱动程序 WDK，虚拟子单位驱动程序
- 虚拟子单位驱动程序 WDK AV/C
- 外部设备 WDK AV/C
- IOCTL_AVC_CLASS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 538e9172b914d9caa995c3aabddc3b43728a3bc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791093"
---
# <a name="virtual-subunit-driver-notes"></a>虚拟子单元驱动程序说明


虚拟子源驱动程序通过使用带有 *Avc.sys* 的 [**IOCTL \_ AVC \_ 类**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)接口，响应来自外部 AV/c 设备的控制、状态和通知 AV/c 请求和命令。

IOCTL \_ AVC \_ CLASS Subfunction 代码 [**AVC \_ 函数 \_ GET \_ 请求**](./avc-function-get-request.md) 和 [**AVC \_ 函数 \_ 发送 \_ 响应**](./avc-function-send-response.md) 是虚拟子单位驱动程序与虚拟驱动程序堆栈的其余部分进行交互的关键机制。 虚拟子单位驱动程序在 MN 的 *Avc.sys* 基础驱动) 程序完成后，将 **AVC \_ 函数 \_ GET \_ 请求** IRP 提交给在其 [**irp \_ \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md)例程 (中Avc.sys\_ \_ \_ 。 每次收到虚拟子单位的请求时，都将调用 **AVC \_ 函数 \_ GET \_ REQUEST** IRP 的 i/o 完成例程。 I/o 完成例程必须根据 AV/C 协议规则) ，在 100 ms (内使用异步 IRP) 的 **AVC \_ 函数 \_ 发送 \_ 响应** 来发送响应 (; 它可以使用请求中包含的 [**AVC \_ 命令 \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb) 结构发送响应。 然后，它必须重新提交 **AVC \_ 函数 \_ GET \_ 请求** IRP，然后才能最后从响应的 i/o 完成例程返回。

虚拟驱动程序堆栈中的子单元驱动程序无法直接将命令发送到外部设备。 对等驱动程序堆栈提供此功能。 不过，虚拟子单位驱动程序可以使用 [**AVC \_ 函数 \_ FIND \_ 对等端 \_ do**](./avc-function-find-peer-do.md)和 [**AVC \_ 函数 \_ 对等 \_ \_ 列表**](./avc-function-peer-do-list.md)subfunctions，来发现和引用 *Avc.sys* 的对等实例，然后与外部 AV/C 子单元连接交互。 [**\_ \_**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

对于每个枚举的虚拟子单位， *Avc.sys* 会创建相应的设备对象。 因此，添加并删除虚拟子单位后， *Avc.sys* 会触发 IEEE 1394 总线重置。 此重置允许 IEEE 1394 总线上的其他设备检测正在计算机上公开的新功能。 虚拟子单位驱动程序基于 *Avc.sys* 实例的注册表设置进行加载，并且可在运行时通过 IOCTL 代码请求进行添加和删除。 请注意， *Avc.sys* 无法区分同一类型的多个虚拟子单元连接，因此添加和删除这些子单元连接将加载并卸载具有最高子单位标识符的相应虚拟子的驱动程序。

虚拟子单位驱动程序可以是厚或精简。 唯一的要求是将其编写为 WDM 驱动程序。 厚驱动程序实现了虚拟设备的大多数（如果不是全部）功能。 瘦驱动程序提供了虚拟设备功能的代理接口，可以是其他驱动程序或用户模式组件。 用户模式与虚拟子单位驱动程序之间的接口是特定于实现的，可通过 IOCTL 代码、专用设备接口 (参阅 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)) 或 [Windows Management Instrumentation](../kernel/implementing-wmi.md) (WMI) 来实现。

即使 \_ 和 MOD \_ 值与 INF 文件中指定的值相同，后者导致 *61883.sys* 的虚拟实例加载。 TYP \_ 和 ID \_ 值是 *Avc.sys* 枚举虚拟子单位时指定的。

虚拟子单位的枚举通过使用 [**ioctl \_ AVC \_ 更新 \_ 虚拟 \_ \_**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)子单位信息、 [**Ioctl \_ AVC \_ 删除虚拟子单位 \_ \_ \_ 信息**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)和 [**IOCTL \_ AVC \_ 总线 \_ 重置**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset) IOCTL 代码来完成。

必须发送正确的 IEEE 1394 IOCTLs、 **IEEE1394 \_ api \_ ADD \_ 虚拟 \_** 设备和 **IEEE1394 \_ api \_ REMOVE \_ 虚拟 \_ 设备** ，才能开始枚举过程。  (IOCTL \_ IEEE1394 \_ API 请求) 子命令的详细信息 \_ 。 *61883* 文件已包含设备标识符 (ID) 用于此目的： V1394 \\ A02D&10001，但自定义 inf 文件中可能会提供不同的标识符。

可以通过使用 INF 文件来静态枚举虚拟子单位的替代方法。

虚拟设备列表项下的每个值都是一个打包的子地址， (子类型和最大标识符组合在一起，如 AV/C 常规规范) 中所述。 与子单位地址相关联的名称并不重要，但它对于该实例必须是唯一的。 以编程方式创建时，将为值名称提供序列号以避免冲突。

例如，若要通过 INF 文件创建单个虚拟调谐器子单位，请使用以下 **AddReg** 指令：

```INF
[Subunit_Device.NT.HW.AddReg]
HKR,%VirtualAvc.DeviceList%,Tuner,0x00000001,0x28 ;0x00000001 = Binary value, 0x28 = Registry key value
```

此指令将 (0x28 的注册表项 \_ 类型0x5 添加到最重要的5位，并将最大的最大标识符) 打包到最不重要的三位，并将其添加。 此处的最大标识符为0x0，表示将有该类型的单个子单位。

**注意**  ：还必须 `%VirtualAvc.DeviceList%` 在子区域的 INF 文件的部分中定义令牌 `[Strings]` 。
