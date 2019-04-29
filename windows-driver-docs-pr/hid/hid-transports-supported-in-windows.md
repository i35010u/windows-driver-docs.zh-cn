---
title: Windows 中支持的 HID 传输方式
description: Windows 支持以下传输方式。
ms.assetid: 03B66788-A930-4C18-A019-CA906634DC4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e70740e3f611510101de9e629397fda1cd2ba28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388790"
---
# <a name="hid-transports-supported-in-windows"></a>Windows 中支持的 HID 传输方式


Windows 支持以下传输方式。

| “传输”    | Windows 7 | Windows 8 | 说明                                                                                                 |
|--------------|-----------|-----------|-------------------------------------------------------------------------------------------------------|
| USB          | 是       | 是       | 追溯到 Windows 2000 的 Windows 操作系统上提供的 USB HID 1.11 + 的支持。       |
| 蓝牙    | 是       | 是       | 追溯到 Windows Vista 的 Windows 操作系统上提供对蓝牙 HID 1.1 + 的支持。 |
| 蓝牙 LE | 否        | 是       | Windows 8 引入了通过蓝牙 LE 的 HID 支持。                                               |
| I2C          | 否        | 是       | Windows 8 通过 I2C 引入了对 HID 支持                                                         |

 

以前版本的 Windows （之前 Windows 7) 也包括了以下支持。

-   HidGame.sys-HID 微型驱动程序适用于游戏端口 （I/O 端口 201） 设备。 HID 类驱动程序创建游戏端口设备的功能的设备对象 (FDO)，并为每个游戏端口设备支持的 HID 集合创建物理设备对象 (PDO)。
-   Gameenum.sys – 游戏端口总线驱动程序。 游戏端口总线驱动程序创建每个游戏端口设备是联结到游戏端口 PDO。

它们现在被视为旧版因为现代 （替换为 USB 和其他新式传输） 的计算机上找不到硬件。

## <a name="recommended-transports-for-keyboards-mice-and-touchpads"></a>键盘、 鼠标和触摸板的建议的传输


下表显示键盘、 鼠标和触摸板的设备的推荐的传输 （如便携式计算机和平板电脑） 的可移植和非可移植系统 （例如-一体和台式机） 上。

| 系统类型                  | 可移植                                 | 非可移植                                |
|------------------------------|------------------------------------------|---------------------------------------------|
| 旧系统               | 内部：PS/2 和外部：USB、 蓝牙 | 内部：不是适用，外部：USB、 蓝牙     |
| 芯片 (SoC) 系统上的系统 | 内部：I2C，外部：USB、 蓝牙  | 内部：I2C，USB 外部：USB、 蓝牙 |

 

[**USB 一般 HID 测试**](https://msdn.microsoft.com/library/windows/hardware/dn942240) Windows 硬件 Lab Kit (HLK) 中介绍了 HidUsb 和 HidClass 驱动程序。 没有 HLK 测试的第三方 HID 微型驱动程序。 
 




