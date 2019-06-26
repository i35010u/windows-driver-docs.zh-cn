---
title: 端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo
description: 端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo
ms.assetid: 9691f47d-1ea8-4ef6-8e0d-57570ff70a16
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
- ConfigInfo
- 端口驱动程序提供 ConfigInfo WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58697e462a94a881caced31c40cfc4d373ee800f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358460"
---
# <a name="port-driver-supplied-configinfo-for-hwscsifindadapter"></a>端口驱动程序提供的适用于 HwScsiFindAdapter 的 ConfigInfo


## <span id="ddk_port_driver_supplied_configinfo_for_hwscsifindadapter_kg"></span><span id="DDK_PORT_DRIVER_SUPPLIED_CONFIGINFO_FOR_HWSCSIFINDADAPTER_KG"></span>


系统端口驱动程序始终设置了以下[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)调用微型端口驱动程序之前*HwScsiFindAdapter*日常用一个指针指向端口\_配置\_信息 ( *ConfigInfo*缓冲区):

-   **长度**到**sizeof**(端口\_配置\_信息)

-   **AdapterInterfaceType**微型端口驱动程序[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)规范

-   **InterruptMode**到**LevelSensitive** PCI 总线或**Latched**对于所有其他总线类型

    如果微型端口驱动程序不包含*HwScsiInterrupt*例程和集，因此， **HwInterrupt**入口点**NULL**的 HW 中\_初始化\_数据，此成员是不相关。

-   **AtdiskPrimaryClaimed**到**TRUE**如果先前加载的驱动程序使用的 I/O 端口范围 0x1F0 到 0x1FF

-   **AtdiskSecondaryClaimed**到**TRUE**如果先前加载的驱动程序使用的 I/O 端口范围 0x170 到 0x17F

-   **NumberOfAccessRanges**到微型端口驱动程序的 HW\_初始化\_数据规范

-   **Dma64BitAddresses**到微型端口驱动程序的 HW\_初始化\_数据规范，如果系统具有 4 GB 以上的物理地址的内存

端口驱动程序还会尝试在系统中，如注册表旧微型端口驱动程序或从插微型端口驱动程序的插管理器填充具有来自其他源的值的以下成员：

-   **SystemIoBusNumber**设置为 I/O 总线的系统分配值

    微型端口驱动程序[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程可以调用的每个总线给定**AdapterInterfaceType**有关的更新值**SystemIoBusNumber**，这可以设置为系统确定的值，如果系统检测到特定的总线上的 HBA 或给定**AdapterInterfaceType**。

-   **AccessRanges**访问类型的元素\_范围，设置使用总线相对**RangeStart**地址和**RangeLength**，以及每个范围是否**RangeInMemory**

    **RangeInMemory**设置为**FALSE**指示一系列端口在 I/O 空间中，而不是内存空间范围。

    端口驱动程序可以提供所需的访问中的所有信息\_范围元素或其设置为 （默认值） 零元素的所有成员。 通常情况下，端口驱动程序提供额外的配置信息，如果它为访问范围内提供了非零值。

    微型端口驱动程序必须映射提供的端口驱动程序和任何总线相对访问范围值[ **ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)和使用映射的逻辑地址值以确定是否另一个驱动程序支持相应的 HBA。 *永远不会*映射，并使用微型端口驱动程序所提供的范围，如果端口驱动程序提供的端口中填充的访问范围元素访问总线上的 HBA\_配置\_信息传递到*HwScsiFindAdapter*例程。 使用微型端口驱动程序所提供地址，端口驱动程序已提供范围的配置信息时可以重置已配置的 HBA，使其失效性，或甚至可能会导致系统无法引导过程。

    有关使用映射的逻辑访问范围的详细信息，请参阅[设置中 HwScsiFindAdapter ConfigInfo](setting-up-configinfo-in-hwscsifindadapter.md)。

-   **BusInterruptLevel**或**BusInterruptVector**

    此成员是不相关，如果微型端口驱动程序不包含[ **HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))例程。

-   **DmaChannel**或**DmaPort**如果 HBA 使用系统 DMA 控制器

    如果 HBA 是总线主机，或使用 PIO，这些成员是不相关。

-   **InitiatorBusId**

    如果输入**InitiatorBusId\[0\]** 具有值为零，微型端口驱动程序可以分配默认值，如果其 HBA 不需要使用由查询 HBA 的特定值。 否则，微型端口驱动程序应使用尽可能分配端口驱动程序的任何非零值。 每个微型端口驱动程序必须更新**InitiatorBusId**规范以匹配其 HBA 的使用，如有必要的查询来确定适当的值 (s) 的 HBA。

    微型端口驱动程序必须按照所指示的值设置为支持的 HBA，每个 SCSI 总线的条目**NumberOfBuses**。

 

 




