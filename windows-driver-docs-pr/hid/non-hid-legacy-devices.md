---
title: 非 HID 旧设备
description: 本部分介绍了非 HID 键盘和鼠标的驱动程序、传输方式和筛选器驱动程序。 这些设备主要以 PS/2 传输方式运行。
ms.assetid: 4726DD47-C22E-4B92-A7BD-EB37BA53496F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8733769a44e5fbda86c942c86cf5931bc6561e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575637"
---
# <a name="non-hid-legacy-devices"></a>非 HID 旧设备


本部分介绍了非 HID 键盘和鼠标的驱动程序、传输方式和筛选器驱动程序。 这些设备主要以 PS/2 传输方式运行。

本部分不包含有关 Sermouse，Windows 系统功能驱动程序了串行老鼠的信息。 请注意，将应用于 I8042prt 操作约束不适用 Sermouse。 此外，较高级别设备筛选器驱动程序不用于与 Sermouse 自定义了串行老鼠的操作。 相反，供应商需要安装设备驱动程序特定于设备的函数。 特定于设备的功能驱动程序和 Sermouse 可以运行在同一时间，相互独立。

## <a name="non-hid-driver-stack"></a>非 HID 驱动程序堆栈


Windows 8 的非 HID 键盘、 鼠标和触摸板硬件使用以下驱动程序堆栈。 仅非-HID 传输协议在 Windows 8 上支持是 PS2。

![非 hid 驱动程序堆栈](images/non-hid-driver-stack.png)

 

 




