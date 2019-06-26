---
title: 注册和注销操作区域处理程序
description: 注册和注销操作区域处理程序
ms.assetid: de40488d-7935-431c-b1f4-87f8aff1125b
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 功能的驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
- 注册操作区域处理程序
- 取消操作区域处理程序
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 108e05dc40b77557de56d72d9f390f78a2b7ba26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355817"
---
# <a name="registering-and-deregistering-an-operation-region-handler"></a>注册和注销操作区域处理程序


ACPI 设备功能驱动程序注册的操作区域处理程序通过调用[ **RegisterOpRegionHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nf-oprghdlr-registeropregionhandler)并提供以下信息：

-   物理设备表示的对象 (PDO) 定义的操作区域的 ACPI 设备。

-   访问，可以是类型*原始*或*加工的。*

    有关详细信息，请参阅[访问操作区域](accessing-an-operation-region.md)

-   区域空间的类型。

    供应商应指定从 0x80 到 0xFF 的供应商定义值。 （小于值 0x80 ACPI 规范定义，保留供内部使用。）

-   指向驱动程序的操作区域处理程序的指针。

    ACPI 驱动程序通过调用驱动程序的操作区域处理程序来访问可操作区域。

-   一个指向*区域的操作上下文*。

    操作区域上下文是特定于设备的并且仅由功能驱动程序。 当 ACPI 驱动程序调用的操作区域处理程序时，它将操作区域上下文传递给处理程序。 通常情况下，它是功能的设备对象 (FDO) 设备扩展。

**RegisterOpRegionHandler**返回功能驱动程序用来唯一标识的操作区域处理程序，仅当该驱动程序中注销该处理程序时的操作区域对象。

通常情况下，驱动程序的操作区域处理程序中注册驱动程序的插调度例程后它在响应中启动 FDO [ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 它会分配处理程序的操作区域上下文后，驱动程序必须注册处理程序。 如果驱动程序会创建一个供应商定义的设备接口，该驱动程序应注册处理程序后启用设备接口。

ACPI 设备功能驱动程序通过调用注销的操作区域处理程序[ **DeRegisterOpRegionHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nf-oprghdlr-deregisteropregionhandler)并提供以下信息：

-   表示定义的操作区域的 ACPI 设备 PDO。

-   操作区域返回的对象的 ACPI 驱动程序时驱动程序已注册的操作区域处理程序。 此对象唯一标识的操作区域处理程序。

通常情况下，驱动程序会向驱动程序的插调度例程中的操作区域处理程序之前它将停止响应 FDO [ **IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求。 它使处理程序的操作区域上下文之前，该驱动程序必须取消注册处理程序。 如果该驱动程序会创建一个供应商定义的设备接口，该驱动程序应禁用设备接口之前注销该处理程序。

 




