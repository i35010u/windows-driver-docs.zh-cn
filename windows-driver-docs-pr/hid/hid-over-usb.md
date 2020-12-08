---
title: 基于 USB 的 HID 概述
description: USB 是 Windows 操作系统中第一个受支持的 HID 传输。
keywords:
- HID 微型端口驱动程序
- USB
- USB 1。1
- USB 2。0
- USB 3.0
- USB，HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7f573551376beb02f3e6cb16518d7ea21698fc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838617"
---
# <a name="hid-over-usb-overview"></a>基于 USB 的 HID 概述

USB 是 Windows 中第一个受支持的 HID 传输。 Windows 2000 中引入了相应的内置驱动程序，自那时起，所有操作系统均提供了该驱动程序。 此驱动程序已经过增强，其中包括从触摸板和键盘到传感器的新类和特定于供应商的设备类型。 USB 上的 HID 还经过优化，可以利用选择性挂起。  (此功能需要供应商通过 Microsoft 操作系统描述符提供的 INF 或支持。 ) 

通过 USB 进行的最新 HID 更新还包括：

- 支持 USB 1.1、USB 2.0 和 USB 3.0。
- Windows 的所有客户端 Sku 上都提供了一个基于 USB 驱动程序的 HID，它包含在 WinPE 中。

## <a name="see-also"></a>请参阅

- [HID USB 主页](https://www.usb.org/hid)
- [HID USB 规范](https://www.usb.org/sites/default/files/documents/hid1_11.pdf)
- [HID 使用情况表](https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf)
