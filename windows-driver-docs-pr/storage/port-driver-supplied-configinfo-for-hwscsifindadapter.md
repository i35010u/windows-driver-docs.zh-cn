---
title: 端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo
description: 端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo
ms.assetid: 9691f47d-1ea8-4ef6-8e0d-57570ff70a16
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- ConfigInfo
- 端口驱动程序提供的 ConfigInfo WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c2d0d689f74c5fe3b91bea1d43904fdd1272f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842727"
---
# <a name="port-driver-supplied-configinfo-for-hwscsifindadapter"></a>端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo


## <span id="ddk_port_driver_supplied_configinfo_for_hwscsifindadapter_kg"></span><span id="DDK_PORT_DRIVER_SUPPLIED_CONFIGINFO_FOR_HWSCSIFINDADAPTER_KG"></span>


系统端口驱动程序在调用微型端口驱动程序的*HwScsiFindAdapter*例程之前，系统端口驱动程序将始终设置以下[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)（通过指向端口\_配置\_信息，*ConfigInfo*缓冲区）：

-   **Length**到**sizeof**（端口\_配置\_信息）

-   **AdapterInterfaceType**到微型端口驱动程序的[**硬件\_初始化\_数据（SCSI）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)规范

-   **InterruptMode** to **LEVELSENSITIVE** for a PCI bus 或所有其他总线类型的**锁定**

    如果微型端口驱动程序没有*HwScsiInterrupt*例程，因此，在\_数据的 HW\_初始化中将**HwInterrupt**入口点设置为**NULL** ，则此成员是不相关的。

-   如果先前加载的驱动程序正在使用 i/o 端口范围0x1F0 到0x1FF，则**AtdiskPrimaryClaimed**为**TRUE**

-   如果先前加载的驱动程序正在使用 i/o 端口范围0x170 到0x17F，则**AtdiskSecondaryClaimed**为**TRUE**

-   **NumberOfAccessRanges**到微型端口驱动程序的 HW\_初始化\_数据规范

-   如果系统具有超过 4 GB 的物理地址的内存， **Dma64BitAddresses**到微型端口驱动程序的硬件\_初始化\_数据规范

端口驱动程序还尝试使用系统中其他源的值（例如，旧版微型端口驱动程序的注册表或即插即用微型端口驱动程序的即插即用管理器）来填充以下成员：

-   **SystemIoBusNumber**设置为 i/o 总线的系统分配值

    对于给定**AdapterInterfaceType**的每个总线，可以为**SystemIoBusNumber**的更新值调用微型端口驱动程序的[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程，也可以将其设置为系统确定的值（如果系统检测到给定**AdapterInterfaceType**的特定总线。

-   类型为 ACCESS\_范围的**AccessRanges**元素，使用与总线相关的**RangeStart**地址和**RangeLength**，以及每个范围是否为**RangeInMemory**

    **RangeInMemory**设置为**FALSE** ，表示 i/o 空间中的一系列端口，而不是内存空间范围。

    端口驱动程序要么提供 ACCESS\_范围元素中的所有信息，要么将元素的所有成员设置为（默认值）零。 通常，如果端口驱动程序为访问范围提供非零值，则它会提供其他配置信息。

    微型端口驱动程序必须将端口驱动程序提供的任何与总线相关的访问范围值映射到[**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase) ，并使用映射的逻辑地址值来确定相应的 HBA 是否为驱动程序支持的端口。 如果端口驱动程序在端口\_配置中提供了已填充的访问范围元素，则*绝不*要映射和使用微型端口驱动程序提供的范围，以便将其传递到*HwScsiFindAdapter*例程的\_信息。 当端口驱动程序提供范围配置信息时，使用微型端口驱动程序提供的地址可以重置已配置的 HBA，使其失效性，甚至会导致系统无法启动进程。

    有关使用映射的逻辑访问范围的详细信息，请参阅[在 HwScsiFindAdapter 中设置 ConfigInfo](setting-up-configinfo-in-hwscsifindadapter.md)。

-   **BusInterruptLevel**或**BusInterruptVector**

    如果微型端口驱动程序没有[**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))例程，则此成员是不相关的。

-   **DmaChannel**或**DMAPORT** （如果 HBA 使用系统 DMA 控制器）

    如果 HBA 为总线主机或使用 PIO，则这些成员不相关。

-   **InitiatorBusId**

    如果输入的**InitiatorBusId\[0\]** 的值为零，则微型端口驱动程序可以分配默认值（如果其 hba 不需要使用通过查询 HBA 确定的特定值）。 否则，微型端口驱动程序应使用端口驱动程序分配的任何非零值（如果可能）。 如果需要查询 HBA 来确定适当的值，则每个微型端口驱动程序必须更新**InitiatorBusId**规范，以匹配其 HBA 使用的内容。

    小型端口驱动程序必须为 HBA 支持的每个 SCSI 总线设置一个条目，如**NumberOfBuses**的值所示。

 

 




