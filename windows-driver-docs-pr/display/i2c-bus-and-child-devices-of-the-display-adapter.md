---
title: 显示适配器的 I2C 总线和子设备
description: 显示适配器的 I2C 总线和子设备
ms.assetid: bfa81f2d-dc35-4430-9117-4706a446058c
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，I2C
- I2C WDK 视频微型端口
- 子设备 WDK 视频微型端口
- I2CRead
- I2CWrite
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d915fa5b88e9096b417e9f92d8688e73cd255d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839653"
---
# <a name="i2c-bus-and-child-devices-of-the-display-adapter"></a>显示适配器的 I2C 总线和子设备


## <span id="ddk_i2c_bus_and_child_devices_of_the_display_adapter_gg"></span><span id="DDK_I2C_BUS_AND_CHILD_DEVICES_OF_THE_DISPLAY_ADAPTER_GG"></span>


显示适配器通常通过 i2c 总线与子设备通信。 例如，监视器是显示适配器的子设备，显示适配器可以通过 I2C 总线读取监视器的功能信息，该总线内置于所有标准的监视器电缆。

I i2c 总线只有两个线路：串行时钟行和串行数据行。 数据从一次一位的行读取和写入。 读取和写入显示适配器上 i2c 行的数据位与硬件相关，因此供应商提供的视频微型端口驱动程序必须提供指示显示适配器读取和写入单个位的函数。

## <a name="i2c-functions"></a>I2C 函数

以下由视频微型端口驱动程序实现的函数，可读取和写入到 I-C 串行时钟和数据行的单个数据位：

* [**ReadClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_clock_line)
* [**ReadDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_data_line)
* [**WriteClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_clock_line)
* [**WriteDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_data_line)

前面的函数必须由调用视频端口驱动程序的[VideoPortDDCMonitorHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportddcmonitorhelper)函数的任何视频微型端口驱动程序实现。

VideoPortDDCMonitorHelper 根据 I2C 规范实现读取监视器的扩展显示标识数据（EDID）的详细信息，但必须依赖于由视频微型端口驱动程序实现的以下功能来读取和写入为 I2C 串行时钟和串行数据线路单独的数据位。

由视频微型端口驱动程序实现的*HwVidGetChildDescriptor*函数负责从特定监视器读取增强的显示标识数据（EDID）结构，并将 EDID 返回到视频端口驱动程序。 *HwVidGetChildDescriptor*可以通过调用**VideoPortDDCMonitorHelper**来获取视频端口驱动程序的帮助，后者使用 I I2c 总线根据显示数据通道（DDC）标准读取监视器的 EDID。 但是，当**VideoPortDDCMonitorHelper**需要读取并写入到 I l I C 时钟和数据行的单个位时，它必须回调到视频微型端口驱动程序以获得帮助。 因此， *HwVidChildDescriptor*将*I2CCallbacks*结构（其中包含指向*ReadClockLine*、 *WriteClockLine*、 *ReadDataLine*和*WriteDataLine*的指针）传递给**VideoPortDDCMonitorHelper**。

## <a name="i2c-functions-implemented-by-the-video-port-driver"></a>由视频端口驱动程序实现的 I2C 函数

I i2c 规范定义了一个协议，该协议用于启动 i2c 通信，并通过 I-C 数据行读取和写入字节，并终止了 i2c 通信。 系统提供的视频端口驱动程序提供了以下用于实现该协议的函数。

* [**I2CStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_start)
* [**I2CRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_read)
* [**I2CWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_write)
* [**I2CStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_stop)

前面列表中的每个函数（已实现但不由视频端口驱动程序导出）都需要视频微型端口驱动程序的帮助。 在视频微型端口驱动程序可以调用 I i2c 函数之前，它必须通过将 VideoPortServicesI2C 传递到[VideoPortQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)函数来获取函数指针。

例如， **I2CRead**函数通过 i2c 数据行读取字节序列，但读取每个字节需要读取8个单个位，这是一个只有视频微型端口驱动程序可以执行的任务。 **I2CRead**函数可获取有关视频微型端口驱动程序的帮助，*因为它会将指向由视频微型端口驱动程序（ReadClockLineWriteClockLine*、 *ReadDataLine*和*WriteDataLine*）。 同样， **I2CStart**、 **I2CRead**和**I2CWrite**分别接收*I2CCallbacks*结构，其中包含指向所有4个视频微型端口驱动程序的 I i2c 函数的指针。


有关所有视频微型端口驱动程序函数和这些函数的注册方式的概述，请参阅[视频微型端口驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/)。

有关 I i2c 总线的详细信息，请参阅由 Philips 半导体发布的 I i2c 总线规范。

 

 





