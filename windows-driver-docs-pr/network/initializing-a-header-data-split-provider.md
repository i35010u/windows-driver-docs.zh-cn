---
title: 初始化标头数据拆分提供程序
description: 初始化标头数据拆分提供程序
keywords:
- 标头-数据拆分 WDK，初始化提供程序
- 初始化标头-数据拆分提供程序
- 标头-数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21f8a577d5ec65370b9da8fcff4fe211102eac01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823881"
---
# <a name="initializing-a-header-data-split-provider"></a>初始化标头数据拆分提供程序





若要支持标头数据拆分，微型端口驱动程序必须注册为 NDIS 6.1 或更高版本的驱动程序。 微型端口驱动程序的源文件必须指定 DNDIS61 \_ 微型端口 = 1 而不是 DNDIS60 \_ 微型端口 = 1。 微型端口驱动程序还必须在 [**ndis \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) 结构中指定 ndis 6.1 或更高版本。

为了注册其标头数据拆分属性，NDIS 6.1 微型端口驱动程序从其 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传递 **NdisMSetMiniportAttributes** 已初始化的 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性结构包含以下信息：

-   NDIS **HDSplitAttributes** \_ 微型端口 \_ 适配器 \_ 硬件辅助属性的 HDSplitAttributes 成员 \_ \_ 包含指向 [**ndis \_ HD \_ SPLIT \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的指针，该结构指定了微型端口适配器提供的标头数据拆分功能。

-   NDIS **HardwareCapabilities** \_ HD SPLIT 属性的 HardwareCapabilities \_ 成员 \_ 包含微型端口适配器支持的标头数据拆分功能。 这些功能可能包括 INF 文件设置当前禁用的功能，或通过 " **高级** 属性" 页禁用的功能。

-   NDIS **CurrentCapabilities** \_ HD SPLIT 属性的 CurrentCapabilities \_ 成员 \_ 包含微型端口适配器支持的当前标头数据拆分功能。 如果通过 **\* HEADERDATASPLIT** 标准化 INF 关键字启用了标头-数据拆分，微型端口驱动程序将使用与 **HardwareCapabilities** 成员相同的标志来指示当前标头-数据拆分配置。 有关 **\* HeaderDataSplit** 的详细信息，请参阅 [Header-Data Split 的标准化 INF 关键字](standardized-inf-keywords-for-header-data-split.md)。

-   NDIS **HDSplitFlags** \_ HD SPLIT 属性的 HDSplitFlags \_ 成员 \_ 包含标头数据拆分配置标志。 在调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)之前，微型端口驱动程序应将此成员设置为零。 NDIS 使用配置标志的按位 "或" 设置此成员。 成功返回 **NdisMSetMiniportAttributes** 后，微型端口驱动程序必须检查 **HDSplitFlags** 中的标志设置，并相应地配置硬件。

NDIS 使用 NDIS \_ HD \_ SPLIT \_ 启用 \_ 标头 \_ 数据 \_ 拆分标志来启用小型端口适配器的标头数据拆分。 \_ \_ \_ \_ \_ \_ 如果微型端口驱动程序未将 ndis hd split cap 设置为 Ndis hd split \_ \_ \_ \_ \_ \_ \_ [**\_ \_ \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的 **CurrentCapabilities** 成员中的标头数据拆分标志，ndis 不会设置 ndis hd 拆分启用标头数据拆分。 如果 NDIS 设置了 NDIS \_ HD \_ split \_ enable \_ 标头 \_ 数据 \_ 拆分标志，微型端口驱动程序应在 NIC 中启用标头数据拆分。

在调用 NdisMSetMiniportAttributes 之前，微型 **BackfillSize** 端口驱动程序应将 NDIS \_ HD 拆分属性结构的 BackfillSize 成员设置 \_ \_ 为零。 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 如果微型端口驱动程序必须在拆分框架的数据缓冲区中预分配回填存储，NDIS 会设置 **BackfillSize** 成员。 成功返回 **NdisMSetMiniportAttributes** 后，微型端口驱动程序必须使用 NDIS 指定的 **BackfillSize** 值并预先分配数据缓冲区。 有关数据缓冲区回填大小的详细信息，请参阅为 [数据缓冲区分配回填](allocating-backfill-for-the-data-buffer.md)。

在调用 **NdisMSetMiniportAttributes** 之前，微型端口驱动程序应将 [**NDIS \_ HD \_ 拆分 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的 **MaxHeaderSize** 成员设置为零。 NDIS 将此成员设置为拆分框架的标头缓冲区允许的最大大小。 成功返回 **NdisMSetMiniportAttributes** 后，微型端口驱动程序必须使用 NDIS 指定的 **MaxHeaderSize** 值。 有关最大标头大小的详细信息，请参阅 [分配标头缓冲区](allocating-the-header-buffer.md)。

 

