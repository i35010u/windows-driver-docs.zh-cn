---
title: 初始化标头数据拆分提供程序
description: 初始化标头数据拆分提供程序
ms.assetid: 19a01906-6a05-4f57-a22a-911138095c84
keywords:
- 标头数据拆分 WDK，初始化提供程序
- 正在初始化标头数据拆分提供程序
- 标头数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e09d4dac20f63abe2fc1d752a62114730331ac3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379813"
---
# <a name="initializing-a-header-data-split-provider"></a>初始化标头数据拆分提供程序





若要支持标头数据拆分，微型端口驱动程序必须注册为 NDIS 6.1 或更高版本的驱动程序。 源文件微型端口驱动程序必须指定 DNDIS61\_微型端口 = 1 而不是 DNDIS60\_微型端口 = 1。 NDIS 6.1 或更高版本中的，还必须指定微型端口驱动程序[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构。

若要注册其标头数据拆分属性，NDIS 6.1 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数从其[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数并传递**NdisMSetMiniportAttributes**初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

NDIS\_微型端口\_适配器\_硬件\_帮助\_属性结构包含以下信息：

-   **HDSplitAttributes**成员的 NDIS\_微型端口\_适配器\_硬件\_协助\_属性包含一个指向[ **NDIS\_HD\_拆分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)结构，它指定标头数据拆分的微型端口适配器提供的功能。

-   **HardwareCapabilities**成员的 NDIS\_HD\_拆分\_属性包含的微型端口适配器支持的标头数据拆分功能。 这些功能可以包括由 INF 文件设置或通过当前已禁用的功能**高级**属性页。

-   **CurrentCapabilities**成员的 NDIS\_HD\_拆分\_属性包含当前的微型端口适配器支持的标头数据拆分功能。 如果通过启用标头数据拆分 **\*HeaderDataSplit**标准化的 INF 关键字，微型端口驱动程序将使用相同的标记作为**HardwareCapabilities**成员以指示当前标头数据拆分配置。 有关详细信息 **\*HeaderDataSplit**，请参阅[标头数据拆分的标准化 INF 关键字](standardized-inf-keywords-for-header-data-split.md)。

-   **HDSplitFlags**成员的 NDIS\_HD\_拆分\_属性包含标头数据拆分配置标志。 微型端口驱动程序应将此成员设置为零，然后再调用[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。 NDIS 设置此成员与配置标志的按位 OR。 之后**NdisMSetMiniportAttributes**成功返回时，微型端口驱动程序必须签入的标志设置**HDSplitFlags**并相应地配置硬件。

NDIS 使用 NDIS\_HD\_拆分\_启用\_标头\_数据\_拆分标志以启用标头数据拆分为微型端口适配器。 NDIS 不会设置 NDIS\_HD\_拆分\_启用\_标头\_数据\_拆分如果微型端口驱动程序未设置 NDIS\_HD\_拆分\_CAPS\_支持\_标头\_数据\_中的拆分标志**CurrentCapabilities**的成员[ **NDIS\_HD\_拆分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)结构。 微型端口驱动程序应启用标头数据拆分的 nic，如果 NDIS 设置 NDIS\_HD\_拆分\_启用\_标头\_数据\_拆分标志。

微型端口驱动程序应设置**BackfillSize**成员的 NDIS\_HD\_拆分\_为零之前调用的属性结构[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。 NDIS 集**BackfillSize**如果微型端口驱动程序必须预分配回填存储数据缓冲区的拆分帧中的成员。 之后**NdisMSetMiniportAttributes**成功返回时，必须使用微型端口驱动程序**BackfillSize**值指定该 NDIS 和预分配数据缓冲区。 有关数据缓冲区回填大小的详细信息，请参阅[数据缓冲区的分配回填](allocating-backfill-for-the-data-buffer.md)。

微型端口驱动程序应设置**MaxHeaderSize**的成员[ **NDIS\_HD\_拆分\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)结构零，然后再调**NdisMSetMiniportAttributes**。 NDIS 此成员设置为允许的标头缓冲区的拆分帧的最大大小。 之后**NdisMSetMiniportAttributes**成功返回时，必须使用微型端口驱动程序**MaxHeaderSize**值指定该 NDIS。 有关最大标头大小的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





