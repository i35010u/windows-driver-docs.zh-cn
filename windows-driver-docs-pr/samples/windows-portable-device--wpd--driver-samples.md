---
title: Windows 便携设备 (WPD) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 WPD 驱动程序的起点。
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: a4c618dc8bafeb30442f3dec42cacf2f10bba921
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831147"
---
# <a name="windows-portable-device-wpd-driver-samples"></a>Windows 便携设备 (WPD) 驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义 WPD 驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [WPD)  (的基本硬件示例驱动程序 ](/samples/microsoft/windows-driver-samples/wpd-basic-hardware-sample-driver-umdf-version-1)  | 一个 WPD 示例驱动程序，该驱动程序支持九个与视差 BS2 可编程微控制器集成的传感器设备。 |
| [Hello World 示例](/samples/microsoft/windows-driver-samples/wpdhelloworld-sample-driver-for-portable-devices) | 此示例驱动程序支持四个对象：设备对象、存储对象、文件夹对象和文件对象。 每个对象都支持一组属性。 |
| [多传输驱动程序](/samples/microsoft/windows-driver-samples/wpd-multi-transport-sample-driver) | 演示如何扩展支持多个传输的设备的 WpdHelloWorldDriver。 传输是便携式设备与计算机进行通信时使用的协议。 示例传输包括 Internet 协议 (IP) 、蓝牙和 USB。 |
| [WPD 服务示例驱动程序](/samples/microsoft/windows-driver-samples/wpd-service-sample-driver) | 演示如何扩展 WpdHelloWorldDriver 示例，使其支持带有联系人设备服务的模拟设备。 |
| [WUDF 驱动程序](/samples/microsoft/windows-driver-samples/wpd-wudf-sample-driver) | 全面的 WPD 示例驱动程序演示了 WPD 设备驱动程序接口的几乎所有方面 (DDI) 。 |
