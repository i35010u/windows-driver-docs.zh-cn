---
title: 非 HID 旧设备
description: 本部分介绍了非 HID 键盘和鼠标的驱动程序、传输方式和筛选器驱动程序。 这些设备主要以 PS/2 传输方式运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c9f9be0c9888da0b24f2a2237e3ee4445ab209
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805613"
---
# <a name="non-hid-legacy-devices"></a>非 HID 旧设备


本部分介绍了非 HID 键盘和鼠标的驱动程序、传输方式和筛选器驱动程序。 这些设备主要以 PS/2 传输方式运行。

本部分不包含有关 Sermouse 的信息，这是用于串行鼠标的 Windows 系统函数驱动程序。 请注意，适用于 I8042prt 的操作约束不适用于 Sermouse。 此外，上层设备筛选器驱动程序不能与 Sermouse 一起用于自定义串行鼠标的操作。 相反，供应商需要安装设备特定的设备驱动程序。 设备特定的函数驱动程序和 Sermouse 可以同时相互操作。

## <a name="non-hid-driver-stack"></a>非 HID 驱动程序堆栈


Windows 8 为非 HID 键盘、鼠标和触摸板硬件使用以下驱动程序堆栈。 Windows 8 上支持的唯一非 HID 传输是 PS2。

![非 hid 驱动程序堆栈](images/non-hid-driver-stack.png)

 

 




