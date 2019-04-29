---
title: Windows 中支持的 HID 客户端
ms.assetid: E6584286-6BF1-40C7-83C1-D07077B13F3E
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22da4c313bc8301660dc9d0ee10f7a8250685347
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388854"
---
# <a name="hid-clients-supported-in-windows"></a>Windows 中支持的 HID 客户端


Windows 支持以下顶级集合：

| **使用情况页面** | **使用情况** | **Windows 7** | **Windows 8** | **Windows 10** | **注意** | **访问模式** |
| --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | 0x0001 - 0x0002 | 是 | 是 | 是 | 鼠标类驱动程序和映射器驱动程序 | 独占 |
| 0x0001 | 0x0004 - 0x0005 | 是 | 是 | 是 | 游戏控制器 | 共享 |
| 0x0001 | 0x0006 - 0x0007 | 是 | 是 | 是 | 键盘 / 键盘类驱动程序和映射器驱动程序 | 独占 |
| 0x0001 | 0x000C | 否 | 是 | 是 | 飞行模式切换 | 共享 |
| 0x0001 | 0x0080 | 是 | 是 | 是 | 系统控件 （电源） | 共享 |
| 0x000C | 0x0001 | 是 | 是 | 是 （对于 Windows 10 和 Windows 10 移动版） | 使用者控件 | 共享 （适用于 Windows 10 和 Windows 10 移动版） |
| 0x000D | 0x0001 | 是 | 是 | 是 | 外部笔设备 | 独占 |
| 0x000D | 0x0002 | 是 | 是 | 是 | 集成的笔设备 | 独占 |
| 0x000D | 0x0004 | 是 | 是 | 是 | Touchscreen | 独占 |
| 0x000D | 0x0005 | 否 | 是 | 是 | 精度触摸板 (PTP) | 独占 |
| 0x0020 | * 多个 | 否 | 是 | 是 | 传感器 | 共享 |
| 0x0084 | 0x004 | 是 | 是 | 是 | HID 的 UPS 电池 | 共享 |
| 0x008C | 0x0002 | 否 | 是 (Windows 8.1 及更高版本) | 是 | 条形码扫描程序 (hidscanner.dll) | 共享 |


在上表中，输入 HID 客户端的访问模式为排他以防止其他 HID 客户端截获或当它们不是该输入的目标接收方时接收全局输入状态。 因此，出于安全原因 RIM （原始输入管理器） 将打开所有此类设备以独占方式。 

共享模式，以允许多个应用程序访问设备。 例如，多个应用程序可以访问条形码扫描程序以查询有关设备功能，并检索统计信息。 不过，检索来自条码扫描器的已解码的数据是以独占模式。 由定义用法[USB HID POS 扫描程序标准规范](https://go.microsoft.com/fwlink/?linkid=830661)。 

* 多个：传感器使用从 0x00 – 0xFF 针对不同目的进行分段。 例如 0x10 指示生物识别的传感器;0x40 指示光线传感器。 这些分配并不连续。 传感器使用实例的列表，请参阅[评审请求 39: HID 用法表传感器页](https://go.microsoft.com/fwlink/?linkid=830659)。 有关支持的 Windows，传感器用法信息[HID 传感器使用](https://go.microsoft.com/fwlink/?linkid=830658)。

 




