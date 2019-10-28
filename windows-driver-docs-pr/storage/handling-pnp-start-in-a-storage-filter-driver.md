---
title: 处理存储筛选器驱动程序中的 PnP 启动
description: 处理存储筛选器驱动程序中的 PnP 启动
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- 存储筛选器驱动程序 WDK、PnP
- 筛选器驱动程序 WDK 存储，PnP
- SFD WDK 存储，PnP
- PnP WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77838cae2f890a6b08e69eb7b1fc5020dec3542d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837554"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>处理存储筛选器驱动程序中的 PnP 启动


## <span id="ddk_handling_pnp_start_in_a_storage_filter_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_FILTER_DRIVER_KG"></span>


存储筛选器驱动程序（SFD）执行特定于设备的初始化，并在 PnP 管理器使用启动请求（[**irp\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)与 IRP\_MN 一起[*调用其设备*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)扩展时，对其进行设置[ **\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)）。 SFD 处理启动请求的方式与存储类驱动程序的处理方式几乎相同。

有关存储类驱动程序如何处理启动请求并设置其设备扩展的信息，请参阅[存储类驱动程序](storage-class-drivers.md)。 有关处理 PnP 开始请求的常规信息，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




