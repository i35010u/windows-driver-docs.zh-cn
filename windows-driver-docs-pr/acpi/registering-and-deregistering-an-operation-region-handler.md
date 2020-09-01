---
title: 注册和注销操作区域处理程序
description: 注册和注销操作区域处理程序
ms.assetid: de40488d-7935-431c-b1f4-87f8aff1125b
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 函数驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
- 注册操作区域处理程序
- 取消注册操作区域处理程序
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 963c8f7a5c6308bd509bbebe4ae14fbdb8b77db6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184497"
---
# <a name="registering-and-deregistering-an-operation-region-handler"></a>注册和注销操作区域处理程序


ACPI 设备函数驱动程序通过调用 [**RegisterOpRegionHandler**](/windows-hardware/drivers/ddi/oprghdlr/nf-oprghdlr-registeropregionhandler) 来注册操作区域处理程序，并提供以下信息：

-   物理设备对象 (PDO) 表示定义操作区域的 ACPI 设备。

-   访问类型，可为 *raw* 或 *加工。*

    有关详细信息，请参阅 [访问操作区域](accessing-an-operation-region.md)

-   区域空间的类型。

    供应商应该指定从0x80 到0xFF 的供应商定义的值。 小于0x80 的 (值由 ACPI 规范定义，并保留供内部使用。 ) 

-   指向驱动程序的操作区域处理程序的指针。

    ACPI 驱动程序通过调用驱动程序的操作区域处理程序来访问操作区域。

-   指向 *操作区域上下文*的指针。

    操作区域上下文是特定于设备的，仅供函数驱动程序使用。 当 ACPI 驱动程序调用操作区域处理程序时，它会将操作区域上下文传递回处理程序。 通常，它是功能设备对象的设备扩展 (FDO) 。

**RegisterOpRegionHandler** 返回一个操作区域对象，函数驱动程序使用该对象唯一标识操作区域处理程序，仅当驱动程序注销该处理程序时。

通常，驱动程序会在启动 FDO 以响应 [**IRP \_ MN \_ START \_ DEVICE**](../kernel/irp-mn-start-device.md) 请求后，在驱动程序的即插即用调度例程中注册一个操作区域处理程序。 驱动程序在分配处理程序的操作区域上下文之后必须注册该处理程序。 如果驱动程序创建供应商定义的设备接口，则驱动程序应在注册处理程序后启用设备接口。

ACPI 设备函数驱动程序通过调用 [**DeRegisterOpRegionHandler**](/windows-hardware/drivers/ddi/oprghdlr/nf-oprghdlr-deregisteropregionhandler) 并提供以下信息来注销操作区域处理程序：

-   表示定义操作区域的 ACPI 设备的 PDO。

-   当驱动程序注册操作区域处理程序时，ACPI 驱动程序返回的操作区域对象。 此对象唯一标识操作区域处理程序。

通常，驱动程序在注销停止 FDO 以响应 [**IRP \_ MN \_ 停止 \_ 设备**](../kernel/irp-mn-stop-device.md) 请求之前，在驱动程序的即插即用调度例程中处理操作区域处理程序。 驱动程序必须先取消对处理程序的注册，然后才能释放处理程序的操作区域上下文。 如果驱动程序创建供应商定义的设备接口，则驱动程序应在注销处理程序之前禁用设备接口。

