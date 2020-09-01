---
title: 对等子单元驱动程序堆栈
description: 对等子的驱动程序堆栈
ms.assetid: 6ef4b6ae-3802-4ba9-acfa-4b3edba11ba3
keywords:
- 对等子单位驱动程序堆栈 WDK AV/C
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- 子次级支持 WDK AV/C
- AV/C WDK，驱动程序堆栈
- 单元命令 WDK AV/C
- 内置扩展机制 WDK AV/C
- 命令扩展机制 WDK AV/C
- 命令面向 WDK AV/C
- Avc.sys 函数驱动程序 WDK，驱动程序堆栈
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1ab9763e409859e7b64c565fcaac06a5c9544d6a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186773"
---
# <a name="peer-subunit-driver-stack"></a>对等子的驱动程序堆栈

对等驱动程序堆栈包含加载的驱动程序，用于表示在 IEEE 1394 总线上处于活动状态并且可从计算机控制的 AV/C 子单元连接。 必须通过 AV/C 对等驱动程序堆栈启动外部设备控制。 每当设备连接到系统 (或在系统) 启动期间存在时，Windows 都会为 IEEE 1394 总线上的每个外部 AV/C 设备加载 *Avc.sys* 的实例。 为支持对等方子驱动程序而加载的每个 *Avc.sys* 实例都注册了 GUID \_ AVC \_ 类设备接口的新实例。 有关 GUID \_ AVC \_ 类设备接口的详细信息，请参阅 [使用 Avc.sys](using-avc-sys.md) 和 [**IOCTL \_ AVC \_ 类**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)。

对等子单位驱动程序通过Avc.sys导出的 IOCTL \_ AVC \_ 类接口*Avc.sys*访问和控制其子单元连接。 *Avc.sys* 处理 AV/C 命令和响应协议，包括与 IEC 61883 函数控制协议的所有交互 (FCP) 。 但请注意，不会阻止对等子驱动程序与进行通信，并在必要时直接访问某些 *61883.sys* 功能。 如果子单位驱动程序代表的 AV/C 子单位使用 Microsoft 不支持的流格式，则它可能需要与 *61883.sys* 直接通信。 必要时，子单位驱动程序可以使用 **IOCTL \_ 61883 \_ 类** 接口直接与 *61883.sys* 进行通信。 Microsoft 提供了较低的筛选器驱动程序 *Avcstrm.sys*，可帮助流式传输 DV 和 MPEG2 格式。 有关 *Avcstrm.sys*的详细信息，请参阅 [AV/C 流式处理概述](av-c-streaming-overview.md)。

对等子源驱动程序可以注册，接收来自外部 AV/C 设备的 AV/C 命令的通知。 若要注册，对等方子驱动程序会发出[**irp \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)i/o 请求数据包 (irp) ， **IoControlCode** \_ 并将 \_ subfunction 设置为 AVC \_ 函数 \_ GET \_ 请求。 此功能允许对等子源驱动程序从其子单位接收 AV/C 请求，并启用对规范的支持，如连接和兼容性管理 (CCM) 协议和数字传输内容保护 (DTCP) 。 有关 CCM 的详细信息，请参阅 [IEEE 1394 贸易关联](https://1394ta.org/library-2/) 网站。 有关 DTCP 的详细信息，请参阅 [数字传输授权管理员](https://www.dtcp.com/) 网站。

请注意，此功能旨在支持虚拟 AV/C 子单元驱动程序，以便将 AV/C 命令发送到计算机 (其中，子计算机驱动程序位于虚拟 AV/C 设备堆栈) 中，而不允许在外部设备上使用 AV/C 子单元连接将 AV/C 命令发送到计算机系统。

## <a name="peer-stack-as-avc-command-target"></a>对等堆栈作为 AV/C 命令目标

对等子单位驱动程序堆栈可以包含其他 WDM 筛选器驱动程序，它们提供特定于供应商或设备特定的目标 AV/C 功能。 通过此对等互连驱动程序堆栈扩展机制，第三方供应商可以独立实现增值功能（如5C 复制保护）以及 Microsoft 提供的 AV/C 实现的扩展。

子单位驱动程序可执行此功能，但对于具有多个子单元连接的设备，WDM 筛选器驱动程序是首选方法。 如果上层驱动程序 (子单位或筛选器驱动程序) 注册，通过 [**AVC \_ 函数 \_ GET \_ 请求**](./avc-function-get-request.md)接收传入请求，则计算机只公开为 AV/C 目标。 有关 AV/C 单元命令的详细信息，请参阅 [**AVC \_ 函数**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)。

驱动程序加载基于)  (Id 的设备标识符;因此，可以在特定于设备或供应商的基础上有选择地加载单元功能。 虚拟子单位驱动程序堆栈支持这种机制 (不) 的特定于设备的方式。

请注意，如果对等子单元驱动程序堆栈实现设备特定的单元扩展，则任何未处理的单元命令以及所有传入的子单位命令都将路由到虚拟子单位 [驱动程序堆栈](virtual-subunit-driver-stack.md)。

## <a name="unit-command-extension-mechanism"></a>单元命令扩展机制

在对等子单元驱动程序堆栈的上下文中，目标功能限制为支持 AV/C 单元命令。 如果某个虚拟子单位或对等方子单位 (的子单位驱动程序) 注册接收 AV/C 请求，则Avc.sys仅支持*Avc.sys*的子 \_ 单位信息 (0x31) 并直接 () \_ 。 有关操作码的详细信息，请参阅 *AV/C 数字接口命令集常规规范 Rev 3.0*。 若要支持其他单元命令（如 CCM 协议或 DTCP 的命令）， *Avc.sys* 提供了插件扩展机制。 任意数量的子单位或 WDM 筛选器驱动程序都可以通过[**AVC \_ 函数 \_ GET \_ REQUEST**](./avc-function-get-request.md)函数提交的[**AVC \_ 命令 \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)结构的**AlternateOpcodes**成员注册其支持的单位操作码。 **AlternateOpcodes** 是计数字节数组;元素0是剩余字节中的替代操作码的数目。 发送响应时将忽略**AlternateOpcodes** ，因此在处理单元请求时不需要隐藏备用操作码。

若要使用内置扩展机制，请在 AVC **SubunitAddress** \_ 命令 IRB 结构的 SubunitAddress 成员中将单位地址指定为 0xff \_ 。 **SubunitAddress**成员在中为单元命令保留 () 的子单位的设备地址仍存在。 虚拟子单位驱动程序始终可以关闭 **SubunitAddress** 成员。