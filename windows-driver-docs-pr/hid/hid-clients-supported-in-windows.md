---
title: Windows 中支持的 HID 客户端
ms.assetid: E6584286-6BF1-40C7-83C1-D07077B13F3E
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 262f2c06758841e92324e9d8b1a0cf15ceb3dcb4
ms.sourcegitcommit: ab45b5ee55705f88ac5f68ef4f45801c687279c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81480745"
---
# <a name="hid-clients-supported-in-windows"></a>Windows 中支持的 HID 客户端


Windows 支持以下顶级集合：

| **使用情况页** | **用法** | **Windows 7** | **Windows 8** | **Windows 10** | **注意** | **访问模式** |
| --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | 0x0001-0x0002 | 是 | 是 | 是 | 鼠标类驱动程序和映射器驱动程序 | 排他 |
| 0x0001 | 0x0004 - 0x0005 | 是 | 是 | 是 | 游戏控制器 | Shared |
| 0x0001 | 0x0006 - 0x0007 | 是 | 是 | 是 | 键盘/键盘类驱动程序和映射器驱动程序 | 排他 |
| 0x0001 | 0x000C | 是 | 是 | 是 | 飞行模式开关 | Shared |
| 0x0001 | 0x0080 | 是 | 是 | 是 | 系统控件（电源） | Shared |
| 0x000C | 0x0001 | 是 | 是 | 是（适用于 Windows 10 和 Windows 10 移动版） | 使用者控件 | 共享（适用于 Windows 10 和 Windows 10 移动版） |
| 0x000D | 0x0001 | 是 | 是 | 是 | 外部笔设备 | 排他 |
| 0x000D | 0x0002 | 是 | 是 | 是 | 集成笔设备 | 排他 |
| 0x000D | 0x0004 | 是 | 是 | 是 | Touchscreen | 排他 |
| 0x000D | 0x0005 | 是 | 是 | 是 | 精度触摸板（PTP） | 排他 |
| 0x0020 | \* 多个 | 是 | 是 | 是 | 传感器 | Shared |
| 0x0084 | 0x004 | 是 | 是 | 是 | HID UPS 电池 | Shared |
| 0x008C | 0x0002 | 是 | 是（Windows 8.1 及更高版本） | 是 | 条形码扫描器（hidscanner） | Shared |


在上表中，输入 HID 客户端的访问模式是独占的，以防止其他 HID 客户端在不是该输入的目标接收方时截获或接收全局输入状态。 因此，出于安全原因，边缘（原始输入管理器）会以独占方式打开所有此类设备。 

共享模式允许多个应用程序访问设备。 例如，多个应用程序可以访问条形码扫描器来查询设备功能和检索统计信息。 但是，从条形码扫描程序中检索已解码的数据在独占模式下完成。 用法由[USB HID POS 扫描器标准规范](https://go.microsoft.com/fwlink/?linkid=830661)定义。 

\* 多：从0x00 –0xFF 的传感器使用情况出于不同目的进行分段。 例如，0x10 表示生物识别传感器;0x40 指示光传感器。 这些分配不是连续的。 有关传感器使用情况的列表，请参阅[复查请求39： HID 使用情况表传感器页面](https://go.microsoft.com/fwlink/?linkid=830659)。 有关 Windows 中支持的传感器使用情况的信息，请[使用 HID 传感器](https://go.microsoft.com/fwlink/?linkid=830658)。

 




