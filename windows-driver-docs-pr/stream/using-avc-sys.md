---
title: 使用 Avc.sys
description: 使用 Avc.sys
ms.assetid: 3b4ec139-ff01-40bd-8e29-92f554180585
keywords:
- Avc.sys 函数驱动程序 WDK，关于 Avc.sys 函数驱动程序
- AV/C WDK，Avc.sys 使用情况
- 子次级支持 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296ebf085d7eb7bc500c8dbb3013fd898fab8388
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191035"
---
# <a name="using-avcsys"></a>使用 Avc.sys





Windows 加载并初始化 *Avc.sys*后， *Avc.sys* 使用标准 AV/c 单元和子单位命令发现连接到 IEEE 1394 总线的所有 AV/c 设备上的活动子单元连接， (包括在计算机是虚拟 AV/c 单元) 时的任何虚拟子单元连接。 然后*Avc.sys*为所有活动的子单元连接生成 (id) 的设备标识符。 接下来， *Avc.sys* 使用标准即插即用 (PnP) 机制为每个次级单位加载相应的子单位驱动程序。 选择要加载的子单位驱动程序时，将基于安装子单位驱动程序的 INF 文件和子单位的设备标识符，由 *Avc.sys* 并在 [AV/C 设备 id](av-c-device-identifiers.md)中介绍。 设备标识符是从 AV/C 设备的单位信息中生成的，与子区域的 ***SubunitType*** 和 ***SubunitID*** 字段结合在一起。 支持子单位的驱动程序可以是特定于供应商的，也可以是子单位类型的通用驱动程序。 例如，大多数 DV 摄像机的子单位驱动程序是 Microsoft 提供的 *Msdv.sys*。

子单位驱动程序通过基于 WDM 体系结构的所有驱动程序所采用的基于标准 IRP 的机制与 *Avc.sys* 进行通信。 子单位驱动程序通过在驱动程序堆栈中分配并将 Irp 发送到 AV/C 协议驱动程序 *Avc.sys*来与其 Av/c 子单位通信。 若要发出 i/o 请求，请包含标头文件 *Avc*，该文件随 Microsoft Windows 驱动程序工具包附带 (WDK) 提供。

子单位驱动程序分配并初始化要由 *Avc.sys*处理的 irp。 子单位驱动程序将 IRP 的 **DeviceIoControl. IoControlCode** 成员设置为对应于所需 AV/C 操作的 IOCTL。

*Avc.sys* 将注册两个 [设备接口](/windows-hardware/drivers/ddi/index)中的一个，具体取决于它加载以支持 (对等机或虚拟) 的子目标驱动程序堆栈。 这些接口定义 *Avc.sys* 导出子单位驱动程序、其他驱动程序以及要使用的应用程序的功能。 然后*Avc.sys*根据驱动程序的 PnP 状态将接口的状态更改为 "已启用" 或 "已禁用"。

*Avc.sys* 将注册 GUID AVC 类的新实例（ \_ \_ 如果已加载它），以提供对对等堆栈)  (外部 AV/C 子单元连接的支持。 此接口仅支持 (IOCTL) 代码的以下 i/o 控件：

-   [**IOCTL \_ AVC \_ 类**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

IOCTL \_ AVC \_ 类反过来支持多个函数代码。 保证 *Avc.sys* 实例的子驱动程序可以通过其父设备对象访问此接口。

GUID \_ AVC \_ 类接口支持所有 IOCTL \_ AVC \_ 类函数代码，但某些函数代码的用法存在限制，如每个函数的参考页中所述。

*Avc.sys* 注册 GUID \_ virtual AVC 类的新 \_ 实例 \_ （如果已加载），以便为虚拟 AV)  (提供对虚拟 stack 的支持。 此接口支持四种 i/o 控制 (IOCTL) 代码：

-   [**IOCTL \_ AVC \_ 类**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

-   [**IOCTL \_ AVC \_ 更新 \_ 虚拟子单位 \_ \_ 信息**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)

-   [**IOCTL \_ AVC \_ 删除 \_ 虚拟子单位 \_ \_ 信息**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)

-   [**IOCTL \_ AVC \_ 总线 \_ 重置**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)

GUID \_ VIRTUAL \_ AVC \_ 类接口不支持每个 IOCTL \_ AVC \_ 类函数代码。 每个单独的函数代码的 "引用" 页指定Avc.sys的 GUID \_ VIRTUAL \_ AVC \_ 类实例*Avc.sys*是否支持此功能。

IOCTL \_ AVC \_ 类 irp 仅在内核模式下受支持 (通常用于通过 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)的驱动程序到驱动程序通信) 。 因此，应用程序不能直接访问 IOCTL \_ AVC \_ 类 ioctl 代码提供的函数。

在内核模式和用户模式下通过 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)支持最后三条 IOCTL 代码。 这意味着，应用程序可以将这些 IOCTLs 直接发送到 *Avc.sys*。

IOCTL \_ AVC \_ 类 ioctl 代码必须始终附带一个 i/o 请求块 (IRB) ，进一步描述要执行的 AV/C 操作。 IRB 标头包含一个函数号，它确定 IRB 的其余部分的结构。 IRB 结构和大小因函数而异。 *Avc.sys* 使用两个自定义 IRBs：

-   [**AVC \_ 命令 \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)

-   [**AVC \_ MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)

子 IRB 驱动程序必须使用的选项取决于所需的函数。 有关 \_Avc.sys 支持的 IOCTL AVC \_ 类函数代码的详细信息 * ，* 请参阅 [AV/C 协议驱动程序函数代码](./av-c-protocol-driver-function-codes.md)。

子单位驱动程序使用的主要 AV/C 函数是 [**AVC \_ function \_ 命令**](./avc-function-command.md)，该命令使用 AVC \_ 命令 \_ IRB 结构。 **AVC \_函数 \_ 命令** 发送 AV/c 请求并接收相应的 Av/c 响应。 用于生成 AV/C 命令的详细信息由 *Avc.sys*处理，但是，子单位驱动程序必须提供每个命令的 AV/C 操作码和操作数。

 

