---
title: SpbAccelerometer 驱动程序概述
description: 此示例 UMDF 驱动程序控制连接到 (SPB) 的简单外围总线的 ADXL345 加速感应。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b4f79ac83aabb8081739459776474714bd5ce18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805095"
---
# <a name="spbaccelerometer-driver-overview"></a>SpbAccelerometer 驱动程序概述


此示例 UMDF 驱动程序控制连接到 (SPB) 的简单外围总线的 ADXL345 加速感应。ADXL345 是可以沿每个轴测量 +/-16g 的低功率、3轴、加速度。 此传感器支持 SPI 传输和 I2C 传输;示例驱动程序支持 I2C 传输。  (可以从 [SparkFun](https://go.microsoft.com/fwlink/p/?linkid=401463)订购 ADXL345 和专题讨论板。 ) 

即使你的系统不支持此传感器，你也可以使用该示例驱动程序作为参考来通过 I2C 集成其他设备。

 

 




