---
title: 人体学接口设备 (HID) 简介
description: 本部分介绍了人机接口设备（或 HID）。 通常情况下，这些设备是人们用来直接控制计算机系统操作的设备。
ms.assetid: 19aefe5f-d82a-411f-86ab-5d1d53191524
keywords:
- 指针设备 WDK
- 输入设备 WDK
- 人机接口设备 WDK
- HID WDK
ms.date: 02/28/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: ad35eabb019b12b4367c7413cc22db98dacd1940
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166681"
---
# <a name="introduction-to-human-interface-devices-hid"></a>人体学接口设备 (HID) 简介

人体学接口设备 (HID) 是一个设备类定义，用于将 PS/2 样式的连接器替换为支持 HID 设备（例如键盘、鼠标、游戏控制器等）的通用 USB 驱动程序。在 HID 之前，设备只能对鼠标和键盘使用严格定义的协议。 硬件创新要求使用现有协议重载数据，或使用其自己的专用驱动程序创建非标准硬件。 HID 为这些“启动模式”设备提供了支持，同时通过可扩展、标准化且易于编程的接口添加对硬件创新的支持。

目前，HID 设备包括各种设备，例如字母数字显示器、条码读取器、扬声器/耳机上的音量控制、辅助显示器、传感器等。 许多硬件供应商还对其专用设备使用 HID。

HID 一开始为 USB，但设计为与总线无关。 它为低延迟、低带宽设备而设计，但可以灵活地指定基础传输中的速率。 1996 年，基于 USB 的 HID 的规范被 [USB-IF](https://www.usb.org/about) 批准。不久之后，对其他传输的支持又获得批准。 有关当前支持的传输的详细信息，可参阅 [Windows 中支持的 HID 传输](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-transports)。 此外，还允许通过自定义传输驱动程序进行第三方的特定于供应商的传输。

## <a name="hid-concepts"></a>HID 概念

HID 包含两个基本概念：“报告描述符”和“报告”。 报告是在设备和软件客户端之间交换的实际数据。 报告描述符描述设备支持的数据的格式和含义。

### <a name="reports"></a>报告

应用程序和 HID 设备通过报告来交换数据。 有三种报告类型：输入报告、输出报告和功能报告。

| 报告类型    | 说明                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| 输入报告   | 从 HID 设备发送到应用程序的数据，通常在控件的状态发生更改时发送。 |
| 输出报告  | 从应用程序发送到 HID 设备（例如键盘上的 LED）的数据。         |
| 功能报告 | 可以手动读取和/或写入的数据，通常与配置信息相关。    |

报告描述符中定义的每个顶级集合可能包含每个类型的零 (0) 个或更多个报告。

### <a name="usage-tables"></a>用法表

[USB-IF](https://www.usb.org/about) 工作组发布的 HID 用法表是描述允许哪些 HID 设备执行操作的报告描述符的组成部分。 这些 HID 用法表包含一个对**用法**进行了描述的列表，描述报告描述符中所述的特定项目的预期含义和用法。 例如，为鼠标的左按钮定义了用法。 报告描述符可以定义应用程序在报告中的何处能够找到鼠标左键的当前状态。 用法表分为多个称为“用法页”的命名空间。 每个用法页描述了一组相关的用法，有助于组织文档。 将用法页和用法组合起来，就可以定义用法 ID，该 ID 可唯一标识用法表中的特定用法。

## <a name="see-also"></a>另请参阅

[USB-IF HID 规范](https://www.usb.org/hid)。
