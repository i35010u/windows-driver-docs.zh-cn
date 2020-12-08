---
title: 通过 USB 进行的 HID 电源管理
description: USB 上的 HID 使用 USB 挂起对设备进行电源管理。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14acca8a76d96ad6f43f46d2f64dca0765cb6e82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820335"
---
# <a name="hid-power-management-over-usb"></a>基于 USB 的 HID 电源管理

USB 上的 HID 使用 USB 挂起对设备进行电源管理。

电源的管理主要分为以下两种配置：

1. 情况 \# 1：系统处于电源托管状态 (例如 S3) ，但设备仍在唤醒系统。 例如 一种 HID USB 键盘，用于在按键时唤醒来自 S3 的桌面。 **注意：** HID 设备不会自动从低功耗状态唤醒系统。 只有特定的 HID 设备 (例如，键盘和鼠标的顶级集合) 执行此操作。 如果最终用户希望 disarm 设备唤醒系统，用户可以通过设备管理器中的 "属性/电源管理" 选项卡来指定此项。

2. 情况 \# 2：系统处于运行状态 (例如 S0) ，但是设备已空闲， (不) 用户交互。 例如 选择性地在没有使用或触摸 HID USB 鼠标时将其挂起。
