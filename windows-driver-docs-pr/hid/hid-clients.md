---
title: HID 客户端概述
description: HID 客户端是使用 HID API 进行通信的驱动程序、服务或应用程序，通常表示特定类型的设备 (例如传感器、键盘或鼠标) 。
keywords:
- HID 客户端
- 驱动程序
- services
- HID API
- HID 集合
ms.date: 02/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 85392170e9c0ae8179ef6d95f1c09ac3cd66c427
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808851"
---
# <a name="hid-clients-overview"></a>HID 客户端概述

用户界面设备 (HID) 客户端是使用 HID API 通信的驱动程序、服务或应用程序，通常表示特定类型的设备，如传感器、键盘或鼠标。 设备由硬件 ID 或特定的 HID 集合标识，并通过 HID API 进行通信。

| 主题 | 描述 |
| --- | --- |
| [HID 用法](./hid-usages.md) | _Hid 用法_ 标识 hid 控件的用途以及控件实际度量的内容。 |
| [HID 集合](./hid-collections.md) | _Hid 集合_ 是一组有意义的 hid 控件及其各自的 [hid 用法](./hid-usages.md) |
| [打开 HID 集合](./opening-hid-collections.md) | 本部分介绍 HID 客户端如何与 HID 类驱动程序通信， (HIDClass) 操作设备的 HID 集合。 |
| [处理 HID 报告](./handling-hid-reports.md) | 本部分介绍用户模式应用程序和内核模式驱动程序用于处理[HID 报表](./introduction-to-hid-concepts.md)的机制 |
| [释放资源](./freeing-resources.md) | 作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。 |
| [安装 HID 客户端](./installing-hid-clients.md) | 本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。 |
| [顶级集合的 HIDClass 硬件 ID](./hidclass-hardware-ids-for-top-level-collections.md) |此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。 |
| [键盘和鼠标 HID 客户端驱动程序](./keyboard-and-mouse-hid-client-drivers.md) | 本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示在 HID 使用情况表中进行标准化并在 Windows 操作系统中实现的第一组 HID 客户端。 |
| [传感器 HID 类驱动程序](./sensor-hid-class-driver.md) | 从 Windows 8 开始，Windows 操作系统包含一个内置的传感器 HID 类驱动程序 ( # A0) ，该驱动程序支持使用 HID 传输进行通信的第11种传感器类型。 |
| [飞行模式无线管理](./airplane-mode-radio-management.md) | 从 Windows 8 开始，Windows 操作系统将通过 HID 为飞行模式无线电管理控制提供支持。 |
| [显示器亮度控制](./display-brightness-control.md) | 从 Windows 8 开始，已添加标准化的解决方案，以允许在便携式计算机上 (外部或嵌入) 的键盘，通过 HID 控制便携式计算机或平板电脑的屏幕亮度。 |
