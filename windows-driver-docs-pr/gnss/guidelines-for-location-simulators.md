---
title: 位置模拟器指南
description: 本部分包含实现位置模拟器驱动程序的指南。
ms.date: 11/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: e702cb4ca7ca411767107ee8da369558633cc897
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831509"
---
# <a name="guidance-for-location-simulators"></a>位置模拟器指南

Microsoft Visual Studio 2013 提供一个 [位置模拟器](/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015&preserve-view=true) ，它与你创建的位置模拟器驱动程序一起工作。 本部分包含实现位置模拟器驱动程序的指南。

> [!IMPORTANT]
> Visual Studio 2015 模拟器不包括地理位置按钮。 这是因为 Windows 10 模拟器中不包含地理位置模拟。 如果需要进行这种类型的模拟，则可以在 Windows 8.1 或更早的操作系统上使用 Visual Studio 2013 模拟器。

## <a name="configure-the-simulator"></a>配置模拟器

若要启用模拟器驱动程序，可 `HKLM\Software\Microsoft\Location` 通过将名为 "SimulatorID" 的字符串值设置为模拟器驱动程序的传感器 ID 来编辑注册表项。

## <a name="clear-data-on-simulator-exit"></a>清除模拟器退出时的数据

当模拟器应用程序退出时，模拟器驱动程序应将状态更改为 "无 \_ 数据" 并发送状态更改事件。

## <a name="how-simulator-data-is-used"></a>如何使用模拟器数据

- 来自模拟器驱动程序的数据仅用于位置模拟器的模拟器会话中。 模拟器数据从不用于正常的应用程序。

- 如果模拟器驱动程序在模拟器中运行时没有数据，则会在位置模拟器中使用来自其他源的数据。

## <a name="related-topics"></a>相关主题

[在模拟器中运行 UWP 应用](/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015&preserve-view=true)
