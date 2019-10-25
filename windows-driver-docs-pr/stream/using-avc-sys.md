---
title: 使用 Avc.sys
description: 使用 Avc.sys
ms.assetid: 3b4ec139-ff01-40bd-8e29-92f554180585
keywords:
- Avc 函数驱动程序 WDK，关于 Avc 函数驱动程序
- AV/C WDK，Avc 用法
- 子次级支持 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f697fc5c418de4515ab45ee46e68f3d2ef97f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841657"
---
# <a name="using-avcsys"></a>使用 Avc.sys





Windows 加载并初始化*Avc*后， *AVC*使用标准 AV/c 单元和子单位命令发现连接到 IEEE 1394 总线的所有 AV/c 设备上的活动子单元连接（包括计算机是虚拟 AV 时的任何虚拟子单元连接）/C unit）。 然后， *Avc*将为所有活动的子单元连接生成设备标识符（id）。 接下来， *Avc*使用标准即插即用（PnP）机制为每个次级单位加载适当的子单位驱动程序。 根据安装子单位驱动程序的 INF 文件以及由*Avc*生成并在[AV/C 设备 id](av-c-device-identifiers.md)中描述的子单位的设备标识符选择要加载的子单位驱动程序。 设备标识符是从 AV/C 设备的单位信息中生成的，与子区域的***SubunitType***和***SubunitID***字段结合在一起。 支持子单位的驱动程序可以是特定于供应商的，也可以是子单位类型的通用驱动程序。 例如，大多数 DV 摄像机的子单位驱动程序是 Microsoft 提供的*Msdv*。

子单位驱动程序通过基于 WDM 体系结构的所有驱动程序所采用的标准 IRP 机制，与*Avc 通信。* 子单位驱动程序通过将 Irp 按驱动程序堆栈分配并发送到 AV/C 协议驱动程序*Avc*来与其 Av/c 子单位通信。 若要发出 i/o 请求，请包括随 Microsoft Windows 驱动程序工具包（WDK）附带的标头文件*Avc。*

子单位驱动程序分配并初始化要由*Avc*处理的 irp。 子单位驱动程序将 IRP 的**DeviceIoControl. IoControlCode**成员设置为对应于所需 AV/C 操作的 IOCTL。

*Avc*将注册两个[设备接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中的一个，具体取决于它加载以支持的子目标驱动程序堆栈（对等或虚拟）。 这些接口定义*Avc*导出的功能，这些功能可供子单位驱动程序、其他驱动程序和应用程序使用。 然后， *Avc*根据驱动程序的 PnP 状态将接口的状态更改为 "已启用" 或 "已禁用"。

如果加载了 Avc 的新实例，并将其加载到提供对外部 AV/C 子单元连接（对等堆栈）的支持，则会将该实例注册到\_类的新\_实例。 此接口仅支持以下 i/o 控制（IOCTL）代码：

-   [**IOCTL\_AVC\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

IOCTL\_AVC\_类反过来支持多个函数代码。 *Avc*实例的子驱动程序以支持对等子单元连接，保证能够通过其父设备对象访问此接口。

GUID\_AVC\_类接口支持所有 IOCTL\_AVC\_类函数代码，但某些函数代码的用法存在限制，如每个函数的参考页中所述。

*Avc*注册\_虚拟\_AVC\_类的 GUID 的新实例（如果已加载），以提供对虚拟 AV/C 子单元连接（虚拟堆栈）的支持。 此接口支持四个 i/o 控制（IOCTL）代码：

-   [**IOCTL\_AVC\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

-   [**IOCTL\_AVC\_更新\_虚拟\_子单位\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)

-   [**IOCTL\_AVC\_删除\_虚拟\_子单位\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)

-   [**IOCTL\_AVC\_总线\_重置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)

GUID\_VIRTUAL\_AVC\_类接口不支持 AVC\_类函数代码的每个\_IOCTL。 每个单独的函数代码的 "引用" 页指定\_虚拟\_AVC\_类实例的 GUID 是否支持*AVC*。

仅在内核模式下（通常用于驱动程序到驱动程序通信）通过[**IRP\_MJ\_内部\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)支持 IOCTL\_AVC\_类 irp。 因此，应用程序不能直接访问 IOCTL\_AVC\_类 IOCTL 代码所提供的函数。

在内核模式和用户模式下，通过[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)同时支持最后三条 IOCTL 代码。 这意味着，应用程序可以将这些 IOCTLs 直接发送到*Avc*。

IOCTL\_AVC\_类 IOCTL 代码必须始终附带 i/o 请求块（IRB），后者进一步描述要执行的 AV/C 操作。 IRB 标头包含一个函数号，它确定 IRB 的其余部分的结构。 IRB 结构和大小因函数而异。 *Avc*使用两个自定义 IRBs：

-   [**AVC\_命令\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)

-   [**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)

子 IRB 驱动程序必须使用的选项取决于所需的函数。 有关 AVC 支持的 IOCTL\_AVC\_类函数代码的详细信息 *，* 请参阅[AV/C 协议驱动程序函数代码](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-protocol-driver-function-codes)。

子单位驱动程序使用的主要 AV/C 函数是[**AVC\_函数\_命令**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-command)，该命令使用 AVC\_命令\_IRB 结构。 **AVC\_函数\_命令**发送 AV/c 请求并接收相应的 Av/c 响应。 用于生成 AV/C 命令的详细信息由*Avc*处理，但子单位驱动程序必须提供每个命令的 AV/C 操作码和操作数。

 

 




