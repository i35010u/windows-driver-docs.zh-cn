---
title: 显示适配器的 I2C 总线和子设备
description: 显示适配器的 I2C 总线和子设备
ms.assetid: bfa81f2d-dc35-4430-9117-4706a446058c
keywords:
- 微型端口驱动程序 WDK Windows 2000 I2C
- I2C WDK 微型端口
- 子设备 WDK 微型端口
- I2CRead
- I2CWrite
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b368336d49a07369c27017358fdc6df8f39399a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566765"
---
# <a name="i2c-bus-and-child-devices-of-the-display-adapter"></a>显示适配器的 I2C 总线和子设备


## <span id="ddk_i2c_bus_and_child_devices_of_the_display_adapter_gg"></span><span id="DDK_I2C_BUS_AND_CHILD_DEVICES_OF_THE_DISPLAY_ADAPTER_GG"></span>


显示适配器通常与子设备通信，通过 I²C 总线。 例如，监视器处于子设备的显示适配器，并显示适配器可以通过 I2C 总线，内置于所有的标准监视器电缆读取监视器的功能信息。

I²C 总线具有只有两个电线： 串行时钟行和串行数据行。 数据是从读取和写入一次行一位。 对读取和写入数据位 I²C 行显示适配器上涉及到硬件，因此，供应商提供微型端口驱动程序必须提供指示显示适配器读取和写入单个位的函数。

## <a name="i2c-functions"></a>I2C 函数

以下函数，由微型端口驱动程序，实现对读取和写入单个数据位 I²C 串行时钟和数据行：

* [**ReadClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_read_clock_line)
* [**ReadDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_read_data_line)
* [**WriteClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_write_clock_line)
* [**WriteDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_write_data_line)

前面的函数必须由调用的视频端口驱动程序的任何视频的微型端口驱动程序实现[VideoPortDDCMonitorHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportddcmonitorhelper)函数。

VideoPortDDCMonitorHelper 实现读取监视器的详细信息扩展显示标识数据 (EDID) 根据 I2C 规范，但必须依赖于以下函数，实现的微型端口驱动程序，以读取和写入I2C 串行时钟和串行数据行到单独的数据位。

*HwVidGetChildDescriptor*函数，由微型端口驱动程序实现负责读取特定监视器的增强型显示标识数据 (EDID) 结构和 EDID 回到视频端口驱动程序。 *HwVidGetChildDescriptor*可以通过调用从视频端口驱动程序获取帮助**VideoPortDDCMonitorHelper**，它使用 I²C 总线读取监视器 EDID 根据显示数据通道 (DDC) 标准。 但是，当**VideoPortDDCMonitorHelper**需要读取或写入到 I²C 时钟和数据行，它必须调用返回到微型端口驱动程序以获得帮助的单个位。 因此， *HwVidChildDescriptor*将传递*I2CCallbacks*结构 (其中包含指向*ReadClockLine*， *WriteClockLine*， *ReadDataLine*，和*WriteDataLine*) 到**VideoPortDDCMonitorHelper**。

## <a name="i2c-functions-implemented-by-the-video-port-driver"></a>视频端口驱动程序实现的 I2C 函数

I²C 规范定义用于启动 I²C 通信、 读取和写入字节过程 I²C 数据行和终止 I²C 通信协议。 系统提供的视频端口驱动程序提供实现该协议的以下函数。

* [**I2CStart**](https://msdn.microsoft.com/library/windows/hardware/ff567375)
* [**I2CRead**](https://msdn.microsoft.com/library/windows/hardware/ff567372)
* [**I2CWrite**](https://msdn.microsoft.com/library/windows/hardware/ff567378)
* [**I2CStop**](https://msdn.microsoft.com/library/windows/hardware/ff567376)

在前面的函数 （实现，但不是导出的视频端口驱动程序） 的每个列表需要协助微型端口驱动程序。 微型端口驱动程序可以调用 I²C 函数之前，它必须以获取函数指针传递到 VideoPortServicesI2C [VideoPortQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueryservices)函数。

例如， **I2CRead**函数通过 I²C 数据行，读取的字节序列，但读取每个字节需要读取八个的单个位，只有微型端口驱动程序可以执行的任务。 **I2CRead**函数可以从微型端口驱动程序获得的帮助，因为它接收的指针 (在*I2CCallbacks*结构) 到由视频微型端口实现的四个 I²C 函数驱动程序 (*ReadClockLine*， *WriteClockLine*， *ReadDataLine*，以及*WriteDataLine*)。 同样， **I2CStart**， **I2CRead**，并**I2CWrite**每个接收*I2CCallbacks*结构，其中包含指向所有四个指针微型端口驱动程序的 I²C 函数。


有关所有微型端口驱动程序功能的概述以及如何注册这些功能，请参阅[视频的微型端口驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff570512)。

I²C 总线的详细信息，请参阅发布 Philips 半导体 I²C 总线规格。

 

 





