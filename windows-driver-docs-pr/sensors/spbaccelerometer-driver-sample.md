---
title: SpbAccelerometer 驱动程序示例
description: 此示例 UMDF 驱动程序控制 ADXL345 加速感应器连接到简单的外围总线 （存储）。
ms.assetid: 5951CED5-13D5-44A4-862A-1C34E2122D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de11b75466a7a170084dae63d517d1bee3664cf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382566"
---
# <a name="spbaccelerometer-driver-sample"></a>SpbAccelerometer 驱动程序示例


此示例 UMDF 驱动程序控制 ADXL345 加速感应器连接到简单的外围总线 （存储）。ADXL345 是低功耗、 3 轴加速感应器能够测量达 + /-16 g 每个轴。

**请注意**  在本部分中的信息适用于 Windows 8.1 和更早的操作系统。 若要评估 Windows 10 和更高版本操作系统的传感器驱动程序示例，请参阅[传感器示例驱动程序](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)。 有关如何开发和生成传感器驱动程序适用于 Windows 10 和更高版本操作系统的信息，请参阅[编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)。

 

传感器永久连接到 I2C 总线假设编写示例。 该驱动程序不支持即插。 相反，硬件平台的 ACPI 系统固件描述传感器设备的总线连接。 插管理器从 ACPI 驱动程序获取总线连接信息、 创建一个连接的 ID 来表示总线连接，并向为硬件资源的示例驱动程序传递的连接 ID。 示例驱动程序使用的连接 ID 以打开到传感器设备的逻辑连接，并获取连接的句柄。 驱动程序指定的目标 I/O 请求将发送到设备的此句柄。

即使您的系统不支持永久连接的 ADXL345 传感器，可以使用此示例作为参考使用，用于将其他设备上存储相集成。

## <a name="related-topics"></a>相关主题
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)  



