---
title: 位置模拟器指南
description: 本部分包含实现位置模拟器驱动程序的指南。
ms.assetid: 4AA6C3EE-0150-45A8-ACC2-D0267591D33D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e0815a0cde1e0e2bbaf58827c8233211662da2f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188907"
---
# <a name="guidance-for-location-simulators"></a>位置模拟器指南


Microsoft Visual Studio 2012 提供一个 [位置模拟器](/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015#bkmk-set-the-simulated-geo-location-of-the-device) ，它与你创建的位置模拟器驱动程序一起工作。 本部分包含实现位置模拟器驱动程序的指南。 请注意，从 Visual Studio 2017 开始，位置模拟器功能不再存在，因此不支持模拟传感器驱动程序。

## <a name="configure-the-simulator"></a>配置模拟器


若要启用模拟器驱动程序，可 `HKLM\Software\Microsoft\Location` 通过将名为 "SimulatorID" 的字符串值设置为模拟器驱动程序的传感器 ID 来编辑注册表项。

## <a name="clear-data-on-simulator-exit"></a>清除模拟器退出时的数据


当模拟器应用程序退出时，模拟器驱动程序应将状态更改为 "无 \_ 数据" 并发送状态更改事件。

## <a name="how-simulator-data-is-used"></a>如何使用模拟器数据


-   来自模拟器驱动程序的数据仅用于位置模拟器的模拟器会话中。 模拟器数据从不用于正常的应用程序。
-   如果模拟器驱动程序在模拟器中运行时没有数据，则会在位置模拟器中使用来自其他源的数据。

## <a name="related-topics"></a>相关主题
[在模拟器中运行 UWP 应用](/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015)  
[设置设备的模拟地理位置](/visualstudio/debugger/run-windows-store-apps-in-the-simulator?view=vs-2015#bkmk-set-the-simulated-geo-location-of-the-device)