---
title: 基于 I i2c 的 HID 电源管理
description: 本部分介绍在 I i2c 上支持 HID 的设备的电源管理。
ms.assetid: 00FE1248-683F-48FE-8422-E51E88224955
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e567781b9ea6a468336c3214eda39109a47927e7
ms.sourcegitcommit: 8835925c6a88efc301dc5e8bd9bca87082416eb6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90777587"
---
# <a name="hid-power-management-over-the-i2c"></a>通过 I2C 进行的 HID 电源管理

本部分介绍了通过 I i2c 传输支持 HID 的设备的电源管理。

## <a name="power-management-and-optimization"></a>电源管理和优化

Windows 8 引入了标有 *Always On、始终连接*的新电源模型。 此模式允许对清单和 Pc 进行优化以实现电源和性能。 同时，在未使用 PC 的情况下，Windows 8is 对能源消耗进行了高度优化。 例如，当屏幕被有意或不是用户活动的结果时，它可以节省电源。

由于 HID 设备是 Windows 中的主要设备类，因此它们必须遵循这一新的电源模式。

### <a name="connected-standby"></a>连接待机

下面简要概述了设备在连接待机电源状态期间的行为方式。

| 输入源                                                                                                                                                    | 指示用户处于连接待机状态 | 处于连接待机状态时处理      | 系统转换到连接待机状态时的设备状态 |
|-|-|-|-|
| 器                                                                                                                                                       | 否                                           | 不得处理                          | D3                                                        |
| 鼠标                                                                                                                                                           | 是                                          | 必须处理，将退出连接待机 | D0                                                        |
| 键盘                                                                                                                                                        | 是                                          | 必须处理，将退出连接待机 | D0                                                        |
| 旋转锁定                                                                                                                                                   | 否                                           | 不得处理                          | D3                                                        |
| 通用桌面控制-将向上移动音量-向下移动-向下移动-向下移动-向下移动一条 | 否                                           | 必须处理                              | D0                                                        |

有关连接备用的详细信息，请参阅 [了解连接待机](https://channel9.msdn.com/events/BUILD/BUILD2011/HW-456T) 视频。

### <a name="supporting-connected-standby-in-hid-ic-devices"></a>支持 HID I i2c 设备中的连接待机

I i2c 总线上的设备是由高级配置和电源接口 (ACPI) 来枚举的。 作为 HID-I i2c 协议规范的一部分，"设置电源" 命令支持 HIDI ²设备的电源管理 \_ 。 此命令指示设备转换为其低功耗模式。

收件箱 HIDI i2c 微型端口驱动程序通过 HIDClass 的 D-IRP 传递。 这样，ACPI 就可以对设备进行电源管理。
