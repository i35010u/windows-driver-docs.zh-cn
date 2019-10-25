---
title: 初始化标头数据拆分提供程序
description: 初始化标头数据拆分提供程序
ms.assetid: 19a01906-6a05-4f57-a22a-911138095c84
keywords:
- 标头-数据拆分 WDK，初始化提供程序
- 初始化标头-数据拆分提供程序
- 标头-数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc4995dc85ec29d87474eb110ee7d0275a899e5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824597"
---
# <a name="initializing-a-header-data-split-provider"></a>初始化标头数据拆分提供程序





若要支持标头数据拆分，微型端口驱动程序必须注册为 NDIS 6.1 或更高版本的驱动程序。 微型端口驱动程序的源文件必须指定 DNDIS61\_微型端口 = 1 而不是 DNDIS60\_微型端口 = 1。 微型端口驱动程序还必须在 Ndis 中指定 NDIS 6.1 或更高版本， [ **\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构。

为了注册其标头数据拆分属性，NDIS 6.1 微型端口驱动程序从其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将**NdisMSetMiniportAttributes**传递到已初始化的[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

NDIS\_微型端口\_适配器\_硬件\_帮助\_属性结构包含以下信息：

-   NDIS\_微型端口\_适配器的**HDSplitAttributes**成员\_硬件\_帮助\_属性包含指向[**NDIS\_HD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)的指针\_用于指定小型端口适配器提供的标头数据拆分功能。

-   NDIS\_HD\_SPLIT\_属性的**HardwareCapabilities**成员包含微型端口适配器支持的标头数据拆分功能。 这些功能可能包括 INF 文件设置当前禁用的功能，或通过 "**高级**属性" 页禁用的功能。

-   NDIS\_HD\_SPLIT\_属性的**CurrentCapabilities**成员包含微型端口适配器支持的当前标头数据拆分功能。 如果通过 **\*HeaderDataSplit**标准化 INF 关键字启用了标头-数据拆分，则微型端口驱动程序将使用与**HardwareCapabilities**成员相同的标志来指示当前标头-数据拆分配置。 有关 **\*HeaderDataSplit**的详细信息，请参阅[用于标头数据拆分的标准化 INF 关键字](standardized-inf-keywords-for-header-data-split.md)。

-   NDIS\_HD\_SPLIT\_属性的**HDSplitFlags**成员包含标头数据拆分配置标志。 在调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)之前，微型端口驱动程序应将此成员设置为零。 NDIS 使用配置标志的按位 "或" 设置此成员。 成功返回**NdisMSetMiniportAttributes**后，微型端口驱动程序必须检查**HDSplitFlags**中的标志设置，并相应地配置硬件。

NDIS 使用 NDIS\_HD\_SPLIT\_启用\_标头\_数据\_SPLIT 标志为微型端口适配器启用标头数据拆分。 NDIS 不会将 NDIS\_HD\_SPLIT\_启用\_标头\_在微型端口驱动程序未将 NDIS\_HD\_剥离\_t_10_ 标头在[**NDIS\_HD\_split\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构的**CurrentCapabilities**成员中\_数据\_split 标志。 如果 NDIS 将 NDIS 设置\_HD\_SPLIT\_启用\_标头\_数据\_拆分标志，则微型端口驱动程序应在 NIC 中启用标头数据拆分。

在调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)之前，微型端口驱动程序应将 NDIS\_HD **\_将\_** 属性结构拆分为零。 如果微型端口驱动程序必须在拆分框架的数据缓冲区中预分配回填存储，NDIS 会设置**BackfillSize**成员。 成功返回**NdisMSetMiniportAttributes**后，微型端口驱动程序必须使用 NDIS 指定的**BackfillSize**值并预先分配数据缓冲区。 有关数据缓冲区回填大小的详细信息，请参阅为[数据缓冲区分配回填](allocating-backfill-for-the-data-buffer.md)。

在调用**NdisMSetMiniportAttributes**之前，微型端口驱动程序应将[**NDIS\_HD\_将\_属性结构拆分**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)为零。 NDIS 将此成员设置为拆分框架的标头缓冲区允许的最大大小。 成功返回**NdisMSetMiniportAttributes**后，微型端口驱动程序必须使用 NDIS 指定的**MaxHeaderSize**值。 有关最大标头大小的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





