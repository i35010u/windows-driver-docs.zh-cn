---
title: HID 客户端概述
description: HID 客户端是使用 HID API 进行通信的驱动程序、服务或应用程序，通常表示特定类型的设备（例如传感器、键盘或鼠标）。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID 客户端
- 驱动程序
- services
- HID API
- HID 集合
ms.date: 02/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9f09cf3cf9b32de247ac10bdbffafdf09b48e089
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223526"
---
# <a name="hid-clients-overview"></a>HID 客户端概述

人体学接口设备（HID）客户端是使用 HID API 通信的驱动程序、服务或应用程序，通常表示特定类型的设备，如传感器、键盘或鼠标。 设备由硬件 ID 或特定的 HID 集合标识，并通过 HID API 进行通信。

| 主题 | 说明 |
| --- | --- |
| [HID 用法](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-usages) | _Hid 用法_标识 hid 控件的用途以及控件实际度量的内容。 |
| [HID 集合](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-collections) | _Hid 集合_是一组有意义的 hid 控件及其各自的[hid 用法](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-usages) |
| [打开 HID 集合](https://docs.microsoft.com/windows-hardware/drivers/hid/opening-hid-collections) | 本部分介绍 HID 客户端如何与 HID 类驱动程序（HIDClass）进行通信，以便操作设备的 HID 集合。 |
| [处理 HID 报告](https://docs.microsoft.com/windows-hardware/drivers/hid/handling-hid-reports) | 本部分介绍用户模式应用程序和内核模式驱动程序用于处理[HID 报表](https://docs.microsoft.com/windows-hardware/drivers/hid/introduction-to-hid-concepts)的机制 |
| [释放资源](https://docs.microsoft.com/windows-hardware/drivers/hid/freeing-resources) | 作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。 |
| [安装 HID 客户端](https://docs.microsoft.com/windows-hardware/drivers/hid/installing-hid-clients) | 本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。 |
| [顶级集合的 HIDClass 硬件 ID](https://docs.microsoft.com/windows-hardware/drivers/hid/hidclass-hardware-ids-for-top-level-collections) |此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。 |
| [键盘和鼠标 HID 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/hid/keyboard-and-mouse-hid-client-drivers) | 本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示在 HID 使用情况表中进行标准化并在 Windows 操作系统中实现的第一组 HID 客户端。 |
| [传感器 HID 类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/hid/sensor-hid-class-driver) | 从 Windows 8 开始，Windows 操作系统包含一个内置的传感器 HID 类驱动程序（SensorsHIDClassDriver），该驱动程序支持使用 HID 传输进行通信的第11种传感器类型。 |
| [飞行模式无线管理](https://docs.microsoft.com/windows-hardware/drivers/hid/airplane-mode-radio-management) | 从 Windows 8 开始，Windows 操作系统将通过 HID 为飞行模式无线电管理控制提供支持。 |
| [显示器亮度控制](https://docs.microsoft.com/windows-hardware/drivers/hid/display-brightness-control) | 从 Windows 8 开始，已添加标准化的解决方案，以允许键盘（外置或嵌入在便携式计算机上）通过 HID 控制便携式计算机或平板电脑的屏幕亮度。 |
