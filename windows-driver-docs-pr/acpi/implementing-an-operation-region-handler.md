---
title: 实现操作区域处理程序
description: 实现操作区域处理程序
ms.assetid: e435393c-d637-45c1-ab65-0b23f796ec02
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 功能的驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33bf2f8820507cd9b8409532f6444b7a30c65c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355838"
---
# <a name="implementing-an-operation-region-handler"></a>实现操作区域处理程序





该驱动程序必须提供的操作区域处理程序，即[ **PACPI\_OP\_区域\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nc-oprghdlr-acpi_op_region_handler)-类型化回调。 ACPI 驱动程序调用的操作处理程序来访问驱动程序的操作区域中的数据字段。 功能驱动程序和 ACPI BIOS 的组合的操作是供应商定义和特定于设备。 一般情况下，功能驱动程序和 ACPI BIOS 访问索引操作的区域中导致特定于设备的操作并返回任何信息正确。

操作区域处理程序通常使用 ACPI 驱动程序将传递给处理程序的以下参数：

-   *AccessType*指定是否读取或写入访问权限。

    如果读取访问，则数据传输到的操作区域内存缓冲区*数据*缓冲区。 如果写入访问，则从传输数据*数据*到操作区域的内存缓冲区的缓冲区。 请参阅[访问的操作区域](accessing-an-operation-region.md)。

-   *地址*操作区域内存缓冲区中指定的字节偏移量。

-   *大小*指定要传输的字节数。

-   *数据*指定由 ACPI 驱动程序提供的数据传输的缓冲区。

-   *上下文*指定驱动程序已注册的操作区域处理程序的操作区域上下文。

    操作区域上下文仅由功能驱动程序，并且是特定于设备的。

除了前面所述参数，ACPI 驱动程序还将传递给以下操作区域的处理程序指针： 操作区域对象、 完成处理程序，并完成上下文。 但是，功能驱动程序不使用的处理程序中的操作区域对象和完成处理程序和上下文保留供内部使用。

 

 




