---
title: 电能表接口
description: 电能表接口
keywords:
- 能源测定和预算 WDK，接口
- 能源指示器接口 WDK
- PMI WDK 能量计量器
ms.date: 11/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 711a8da354ced12f3ba487f415c5bc8de7cf5ac2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191907"
---
# <a name="energy-meter-interface"></a>电能表接口

从 Windows 10 开始，驱动程序可以 (EMI) 实现能量计量接口，以便向客户端公开能源消耗数据。 此接口包含一组标准化的 IOCTLs，可供客户端获取能源数据以及有关计量硬件和正在计量的硬件的数据。 

板上的能源计量会定期衡量导轨上的电压和电流，计算电源，并集成随时间推移使用的总能量。 这些计量不同于现有的 [电源指示器接口](./power-meter-interface.md) 概念，因为电源计量器具有全局平均间隔。 能源计量允许多个使用者根据其需求，通过返回当前的总能耗来确定不同间隔的平均功率。  

EMI 接口为感兴趣的客户端应用程序和服务提供要使用的能源数据的管道。  客户端通过从最新值减去以前的值，计算自上次查询以来消耗的能源，并选择性地将其转换为 "简单" 划分的平均功率。 

## <a name="discovering-devices-that-implement-emi"></a>发现实现了 EMI 的设备

客户端通过调用 [SetupDiEnumDeviceInterfaces](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 和 [SETUPDIGETDEVICEINTERFACEDETAIL](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)发现支持 EMI 的设备。 系统会为每个符合 EMI 标准的能源计量设备创建一个 EMI 设备接口实例。 

EMI 设备接口的 GUID 是在45BD8344-7ED6-49cf-A440-C276C933B053 中定义的 **{}**。 代码还可以使用 GUID_DEVICE_ENERGY_METER 来指定此 GUID。 

## <a name="using-the-emi-interface"></a>使用 EMI 接口

通常，客户端代码使用以下过程与 EMI 交互：

1. 调用 [IOCTL_EMI_GET_VERSION](/windows/desktop/api/emi/ni-emi-ioctl_emi_get_version) 并验证设备支持的 EMI 接口版本是否在返回的 [EMI_VERSION](/windows/desktop/api/emi/ns-emi-emi_version) 值中。 在 Windows 10 中，设备可以支持 EMI_VERSION_V1。 在 Windows 10 版本1809中，设备还可以支持 EMI_VERSION_V2。 将来的操作系统版本可能会引入更高版本。 

2. 调用 IOCTL_EMI_GET_METADATA_SIZE 以获取 EMI 元数据的大小。 

3. 分配所需的 EMI 元数据大小的缓冲区，并调用 [IOCTL_EMI_GET_METADATA](/windows/desktop/api/emi/ni-emi-ioctl_emi_get_metadata)。 验证返回的 EMI_MEASUREMENT_UNIT 是 EmiMeasurementUnitPicowattHours。 Windows 10 之后的版本可以定义其他单位类型。 

4. 若要测量总能耗，请调用 [IOCTL_EMI_GET_MEASUREMENT](/windows/desktop/api/emi/ni-emi-ioctl_emi_get_measurement)。 返回 [EMI_CHANNEL_MEASUREMENT_DATA 结构](/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data) 中的 AbsoluteEnergy 值是 picowatt-小时中具有一些任意零点的总累计能量。 通常情况下，需要在两个不同时间对样本进行比较，并在该间隔内减去能耗的能耗值。 

5. 若要测量平均功率消耗，请在所需间隔的开始和结束时调用 [IOCTL_EMI_GET_MEASUREMENT](/windows/desktop/api/emi/ni-emi-ioctl_emi_get_measurement) 。 减去后一示例所返回的 [EMI_CHANNEL_MEASUREMENT_DATA 结构](/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data) 的 AbsoluteEnergy 和 AbsoluteTime 值。

有关详细信息，请参阅这些主题。

[EMI IOCTLs](/previous-versions/windows/hardware/drivers/dn957425(v=vs.85)) -本部分介绍了 (EMI) EMI 的)  (IOCTLs 的 i/o 控制代码。
 
[EMI 枚举和结构](/previous-versions/windows/hardware/drivers/dn957424(v=vs.85)) -本部分介绍了 (EMI) 的能源测定接口支持的枚举和结构。
 


