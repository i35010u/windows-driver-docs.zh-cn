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
ms.openlocfilehash: 4fb475c9a7926554484fe01cec47e113c9b9060f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064110"
---
# <a name="i2c-bus-and-child-devices-of-the-display-adapter"></a>显示适配器的 I2C 总线和子设备


## <span id="ddk_i2c_bus_and_child_devices_of_the_display_adapter_gg"></span><span id="DDK_I2C_BUS_AND_CHILD_DEVICES_OF_THE_DISPLAY_ADAPTER_GG"></span>


显示适配器通常通过 i2c 总线与子设备通信。 例如，监视器是显示适配器的子设备，显示适配器可以通过 I2C 总线读取监视器的功能信息，该总线内置于所有标准的监视器电缆。

I i2c 总线只有两个线路：串行时钟行和串行数据行。 数据从一次一位的行读取和写入。 读取和写入显示适配器上 i2c 行的数据位与硬件相关，因此供应商提供的视频微型端口驱动程序必须提供指示显示适配器读取和写入单个位的函数。

## <a name="i2c-functions"></a>I2C 函数

以下由视频微型端口驱动程序实现的函数，可读取和写入到 I-C 串行时钟和数据行的单个数据位：

* [**ReadClockLine**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_clock_line)
* [**ReadDataLine**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_data_line)
* [**WriteClockLine**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_clock_line)
* [**WriteDataLine**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_data_line)

前面的函数必须由调用视频端口驱动程序的 [VideoPortDDCMonitorHelper](/windows-hardware/drivers/ddi/video/nf-video-videoportddcmonitorhelper) 函数的任何视频微型端口驱动程序实现。

VideoPortDDCMonitorHelper 根据 I2C 规范实现 (EDID) 读取监视器的扩展显示标识数据的详细信息，但必须依赖于由视频微型端口驱动程序实现的以下功能，以便读取和写入 I2C 串行时钟和串行数据行的单个数据位。

由视频微型端口驱动程序实现的 *HwVidGetChildDescriptor* 函数负责从特定监视器读取 (edid) 结构的增强显示标识数据，并将 edid 返回到视频端口驱动程序。 *HwVidGetChildDescriptor* 可以通过调用 **VideoPortDDCMonitorHelper**来获取视频端口驱动程序的帮助，后者使用 I I2c 总线根据显示数据通道 (DDC) 标准来读取监视器的 EDID。 但是，当 **VideoPortDDCMonitorHelper** 需要读取并写入到 I l I C 时钟和数据行的单个位时，它必须回调到视频微型端口驱动程序以获得帮助。 因此， *HwVidChildDescriptor* 将传递一个 *I2CCallbacks* 结构 (其中包含指向 *ReadClockLine*、 *WriteClockLine*、 *ReadDataLine*和 *WriteDataLine*) 的指针到 **VideoPortDDCMonitorHelper**。

## <a name="i2c-functions-implemented-by-the-video-port-driver"></a>由视频端口驱动程序实现的 I2C 函数

I i2c 规范定义了一个协议，该协议用于启动 i2c 通信，并通过 I-C 数据行读取和写入字节，并终止了 i2c 通信。 系统提供的视频端口驱动程序提供了以下用于实现该协议的函数。

* [**I2CStart**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_start)
* [**I2CRead**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_read)
* [**I2CWrite**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_write)
* [**I2CStop**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_stop)

上述列表中 (实现但不是由视频端口驱动) 程序导出的每个函数都需要视频微型端口驱动程序的帮助。 在视频微型端口驱动程序可以调用 I i2c 函数之前，它必须通过将 VideoPortServicesI2C 传递到 [VideoPortQueryServices](/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices) 函数来获取函数指针。

例如， **I2CRead** 函数通过 i2c 数据行读取字节序列，但读取每个字节需要读取8个单个位，这是一个只有视频微型端口驱动程序可以执行的任务。 **I2CRead**函数可从视频微型端口驱动程序获取帮助，因为它接收到*I2CCallbacks*结构中 (的指针) 到由*ReadClockLine*、 *WriteClockLine*、 *ReadDataLine*和*WriteDataLine*) 的视频微型端口驱动 (程序实现的四个 i2c 函数。 同样， **I2CStart**、 **I2CRead**和 **I2CWrite** 分别接收 *I2CCallbacks* 结构，其中包含指向所有4个视频微型端口驱动程序的 I i2c 函数的指针。


有关所有视频微型端口驱动程序函数和这些函数的注册方式的概述，请参阅 [视频微型端口驱动程序函数](/windows-hardware/drivers/ddi/video/)。

有关 I i2c 总线的详细信息，请参阅由 Philips 半导体发布的 I i2c 总线规范。

 

