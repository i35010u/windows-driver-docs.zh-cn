---
title: 使用 I2C 来与子设备通信
description: 使用 I2C 来与子设备通信
ms.assetid: 5eea2257-49ca-4d76-a6a1-91401595750f
keywords:
- I2C WDK 微型端口
- 微型端口驱动程序 WDK Windows 2000 中，子设备
- 子设备 WDK 微型端口，使用 I2C 进行通信
- 微型端口驱动程序 WDK Windows 2000 I2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca16732dce96828cc1eb1f29f04eaba2c833108d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389013"
---
# <a name="using-i2c-to-communicate-with-a-child-device"></a>使用 I2C 来与子设备通信


## <span id="ddk_using_i2c_to_communicate_with_a_child_device_gg"></span><span id="DDK_USING_I2C_TO_COMMUNICATE_WITH_A_CHILD_DEVICE_GG"></span>


Microsoft Windows XP 及更高版本，插管理器具有枚举视频适配器的子设备后，微型端口驱动程序能够与适配器的子设备上*I2C*总线使用 I²C 协议。 通过公开的微型端口驱动程序软件界面进行微型端口驱动程序和 I²C 总线上的这些设备的 WDM 驱动程序之间的通信 (如中所述[与子设备的驱动程序通信](communicating-with-the-driver-of-a-child-device.md))。 微型端口驱动程序可以启动新的硬件接口公开的视频端口驱动程序通过 I²C 总线上的这些设备之间的物理通信。 如果微型端口驱动程序需要 I²C 主设备 （通常在图形芯片） 进行读写到物理子设备通过 I²C 总线，它可以使用提供的视频端口驱动程序的硬件 I²C 界面[ **VideoPortQueryServices** ](https://msdn.microsoft.com/library/windows/hardware/ff570337)例程。 请注意，这种通信通过 I²C 总线严格限于同一 I²C 总线上的硬件设备。 强烈建议，这些例程用于所有此类通信的微型端口驱动程序编写人员。

这种模式也是通信的有用的视频适配器具有的组件没有任何 WDM 驱动程序的情况。 例如，视频适配器可能具有子板或用于将视频图像发送到数字平板的线路。 微型端口驱动程序可以进行这种情况下，使用提供的硬件 I²C 界面**VideoPortQueryServices** I²C 总线通过将命令发送到该线路。

![说明与通过内部集成电路 (i2c) 接口的子设备通信的关系图](images/i2cfig1.png)

上图说明了如何微型端口驱动程序可以启动 I²C 总线上的两个硬件设备之间的通信。

若要充分利用的视频端口 I²C 例程，微型端口驱动程序必须查询 I²C 接口的视频端口驱动程序。 为此做好准备，微型端口驱动程序必须分配[**视频\_端口\_I2C\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff570538)结构，并初始化其前两个成员 (**大小**并**版本**成员) 为相应的值。 然后，微型端口驱动程序调用的视频端口驱动程序[ **VideoPortQueryServices** ](https://msdn.microsoft.com/library/windows/hardware/ff570337)例程中，设置*servicesType*参数**VideoPortServicesI2C**，并设置*pInterface*参数部分初始化视频\_端口\_I2C\_接口结构。

如果在调用**VideoPortQueryServices**是成功，视频端口驱动程序会填写视频的其余成员\_端口\_I2C\_接口结构，包括四个地址I²C 例程：[**I2CStart**](https://msdn.microsoft.com/library/windows/hardware/ff567375)， [ **I2CStop**](https://msdn.microsoft.com/library/windows/hardware/ff567376)， [ **I2CRead**](https://msdn.microsoft.com/library/windows/hardware/ff567372)，和[ **I2CWrite**](https://msdn.microsoft.com/library/windows/hardware/ff567378).

*I2CStart*并*I2CStop* ，分别使用，来启动与子设备通信并终止与其通信。

*I2CRead*从子设备; 读取指定的字节数*I2CWrite*向其中写入指定的字节数。

 

 





