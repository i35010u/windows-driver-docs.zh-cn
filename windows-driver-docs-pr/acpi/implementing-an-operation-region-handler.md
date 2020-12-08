---
title: 实现操作区域处理程序
description: 实现操作区域处理程序
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 函数驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6e82545d18188d14d671de05aee390bc16a3d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785065"
---
# <a name="implementing-an-operation-region-handler"></a>实现操作区域处理程序





驱动程序必须提供操作区域处理程序，该处理程序是 [**PACPI \_ OP \_ 区域 \_ 处理**](/windows-hardware/drivers/ddi/oprghdlr/nc-oprghdlr-acpi_op_region_handler)程序类型的回调。 ACPI 驱动程序调用操作处理程序来访问驱动程序的操作区域中的数据字段。 函数驱动程序和 ACPI BIOS 的组合操作是供应商定义的和设备特定的。 通常，在操作区域中，函数驱动程序和 ACPI BIOS 访问索引会导致设备特定的操作并返回任何适当的信息。

操作区域处理程序通常使用 ACPI 驱动程序传递给处理程序的以下参数：

-   *AccessType* 指定访问是读取还是写入。

    如果访问是读取，则会将数据从操作区域内存缓冲区传输到 *数据* 缓冲区。 如果访问是写入，数据将从 *数据* 缓冲区传输到操作区域内存缓冲区。 请参阅 [访问操作区域](accessing-an-operation-region.md)。

-   *Address* 指定操作区域内存缓冲区中的字节偏移量。

-   *Size* ：指定要传输的字节数。

-   *数据* 指定 ACPI 驱动程序为数据传输提供的缓冲区。

-   *Context* 指定驱动程序为操作区域处理程序注册的操作区域上下文。

    操作区域上下文仅供函数驱动程序使用，并特定于设备。

除了前面所述的参数外，ACPI 驱动程序还会将操作区域处理程序指针传递到以下内容：操作区域对象、完成处理程序和完成上下文。 但是，函数驱动程序不会在处理程序中使用操作区域对象，并保留完成处理程序和上下文以供内部使用。

 

