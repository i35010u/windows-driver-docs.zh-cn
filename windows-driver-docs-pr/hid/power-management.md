---
title: 通过 USB hid 标准的电源管理
description: 通过 USB HID 的使用 USB 挂起到电源管理设备。
ms.assetid: 7B5E10B0-2EEA-450A-9E21-B60215F60027
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abfbee9b5a0d8c17b89137c99e212a2781cbfff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365435"
---
# <a name="power-management"></a>电源管理


通过 USB HID 的使用 USB 挂起到电源管理设备。

电源管理主要在以下两种配置：

1.  用例\#1:系统处于电源管理状态 (例如 S3)，但设备知识来唤醒系统。 例如 一个知识来唤醒从 S3 按键上桌面的 HID USB 键盘。
2.  用例\#2:系统处于运行状态 (例如 S0)，但该设备已处于空闲状态 （没有用户交互）。 例如 选择性时没有人使用的是或与其相接触挂起 HID USB 鼠标。

*用例\#1 会预配*

HID 的设备不会自动唤醒系统从低功耗状态。 仅特定 HID 设备 （例如顶部级别集合的键盘和鼠标） 执行此操作。

如果最终用户想要清除的设备唤醒系统，用户可以指定这通过在设备管理器中的属性/电源管理选项卡。

 

 




