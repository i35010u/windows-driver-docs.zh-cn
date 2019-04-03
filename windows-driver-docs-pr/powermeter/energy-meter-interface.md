---
title: 电能表接口
description: 电能表接口
keywords:
- 能源计量和预算 WDK 接口
- 能源计量接口 WDK
- PMI WDK 能源计量
ms.date: 11/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 563e23a23e6d6d61c9ce503cb856aa07376296a7
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845534"
---
# <a name="energy-meter-interface"></a>电能表接口

从 Windows 10 开始，驱动程序可以实现能源计量接口 （电磁干扰） 向客户端的能源消耗数据。 此接口包含一组标准化 Ioctl 供客户端获取能耗数据以及数据的计数的硬件和正在按流量计费的硬件。 

板载能源计量定期度量电压和上一个轨道的当前，计算 power 产品，并将随着时间的推移消耗的总能量相集成。 这些指标都不同于现有[电源计量接口](https://docs.microsoft.com/windows-hardware/drivers/powermeter/power-meter-interface)概念因为电表具有全局的平均时间间隔。 能源计量允许多个使用者来确定在根据其需求的不同时间间隔内的平均能源，通过返回到当前的总能量消耗。  

电磁干扰接口提供了用于能源使用相关的客户端应用程序和服务的数据的通道。  客户端计算自其上次查询以来使用的最新值，从以前的值中减去的能源，并根据需要通过将转换为平均能源简单除法。 

## <a name="discovering-devices-that-implement-emi"></a>发现实现电磁干扰的设备

客户端发现的设备，支持通过调用电磁干扰[SetupDiEnumDeviceInterfaces](https://msdn.microsoft.com/library/windows/hardware/ff551015.aspx)并[SetupDiGetDeviceInterfaceDetail](https://msdn.microsoft.com/library/windows/hardware/ff551120.aspx)。 为每个计量电磁干扰符合标准，并在系统中存在的设备的能源创建电磁干扰设备接口的一个实例。 

电磁干扰设备接口的 guid **{45BD8344-7ED6-49cf-A440-C276C933B053}** emi.h 中定义。 或者，代码可以使用 GUID_DEVICE_ENERGY_METER 来指定此 GUID。 

## <a name="using-the-emi-interface"></a>使用电磁干扰接口

客户端代码通常与电磁干扰，使用以下过程进行交互：

1. 调用[IOCTL_EMI_GET_VERSION](https://msdn.microsoft.com/library/windows/hardware/dn957440.aspx) ，并检查在返回设备支持的电磁干扰界面版本[EMI_VERSION](https://msdn.microsoft.com/library/windows/hardware/dn957430.aspx)值。 在 Windows 10 设备可以支持 EMI_VERSION_V1。 在 Windows 10 版本 1809，设备还可以支持 EMI_VERSION_V2。 将来的操作系统版本可能会带来更高版本。 

2. 调用 IOCTL_EMI_GET_METADATA_SIZE 获取电磁干扰元数据的大小。 

3. 分配的所需的电磁干扰元数据大小和调用缓冲区[IOCTL_EMI_GET_METADATA](https://msdn.microsoft.com/library/windows/hardware/dn957436.aspx)。 验证返回的 EMI_MEASUREMENT_UNIT EmiMeasurementUnitPicowattHours。 Windows 10 后的版本可能会定义额外的单位类型。 

4. 若要测量总能源消耗，调用[IOCTL_EMI_GET_MEASUREMENT](https://msdn.microsoft.com/library/windows/hardware/dn957434.aspx)。 在返回的 AbsoluteEnergy 值[EMI_CHANNEL_MEASUREMENT_DATA 结构](https://docs.microsoft.com/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data)是 picowatt 小时与一些任意的零点内的总累计的能量。 一般情况下，您需要在两个不同的时间比较示例，并将该间隔内的能源消耗能源值相减。 

5. 若要测量的平均能源消耗，请调用[IOCTL_EMI_GET_MEASUREMENT](https://msdn.microsoft.com/library/windows/hardware/dn957434.aspx)开头和末尾所需的间隔。 AbsoluteEnergy 和 AbsoluteTime 值中减去[EMI_CHANNEL_MEASUREMENT_DATA 结构](https://docs.microsoft.com/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data)从这些文章的示例返回由后者的示例。

有关详细信息，请参阅以下主题。

[电磁干扰 Ioctl](https://msdn.microsoft.com/library/windows/hardware/dn957425.aspx) -本部分介绍支持的能源度量接口 （电磁干扰） 的 I/O 控制代码 (Ioctl)。
 
[电磁干扰枚举和结构](https://msdn.microsoft.com/library/windows/hardware/dn957424.aspx)-本部分介绍枚举和结构所支持的能源度量接口 （电磁干扰）。
 


 




