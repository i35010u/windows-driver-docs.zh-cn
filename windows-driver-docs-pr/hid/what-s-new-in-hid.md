---
title: 什么是 HID 中的新增功能
description: 本主题总结了新功能和改进的人机接口设备 (HID) 在 Windows 10。
Search.SourceType: Video
ms.assetid: AA8590B4-AAEA-4D41-972F-38149CE328E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a267b4477edf11779e36af9533e0d1976e83de7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520812"
---
# <a name="whats-new-in-hid"></a>什么是 HID 中的新增功能


本主题总结了新功能和改进的人机接口设备 (HID) 在 Windows 10。

## <a name="hid-winrt-api"></a>HID 的 WinRT API


[Windows.Devices.HumanInterfaceDevice](https://msdn.microsoft.com/library/windows/apps/xaml/dn263140) API 来支持人机接口设备 (HID) 协议的 UWP 应用访问设备。

以下简短视频介绍了可供下载 MSDN 示例库上的 HID 端到端示例的解决方案。 （此解决方案包括使用新的 HID WinRT API 创建的示例应用。）

>[!VIDEO https://www.microsoft.com/videoplayer/embed/2d4da9fc-c2ea-4933-949d-eb0cff3c9c4e]

## <a name="design-guide"></a>设计指南

[设计指南](index.md)已更新以包含一些新的主题。 此外，现有的内容已进行了修订的相关，若要在 Windows 10 中显示改进的 HID 支持。 下面是一些新的和更新的主题：

**新主题**

-   [ACPI 按钮设备](acpi-button-device.md)

**已更新的主题**

-   [HID 传输方式](hid-transports.md)

-   [HID 的按钮驱动程序](buttons.md)

-   [在 Windows 中受支持的 HID 客户端](hid-clients-supported-in-windows.md)

## <a name="hid-over-ic"></a>HID Over I²C


HID 协议最初目标等人机接口设备： 键盘、 鼠标和游戏杆。 最初开发时可以在 USB 上运行。 对于 Windows 8 中，Microsoft 创建新的 HID 微型端口驱动程序允许设备通过 Inter-Integrated 线路 (I²C) 总线进行通信。

## <a name="related-topics"></a>相关主题
[设计指南](index.md)  
[HID Over I2C](hid-over-i2c-guide.md)  



