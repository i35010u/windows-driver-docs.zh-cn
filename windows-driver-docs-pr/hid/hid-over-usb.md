---
title: 基于 USB 的 HID 概述
description: USB 是 Windows 操作系统中第一个受支持的 HID 传输。
ms.assetid: F892C910-BA33-4795-A803-9D3FD55782BC
keywords:
- HID 微型端口驱动程序
- USB
- USB 1。1
- USB 2.0
- USB 3.0
- USB，HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 693dc815278f8b692a9529aa37a460163b029db1
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166663"
---
# <a name="hid-over-usb-overview"></a>基于 USB 的 HID 概述

USB 是 Windows 中第一个受支持的 HID 传输。 Windows 2000 中引入了相应的内置驱动程序，自那时起，所有操作系统均提供了该驱动程序。 此驱动程序已经过增强，其中包括从触摸板和键盘到传感器的新类和特定于供应商的设备类型。 USB 上的 HID 还经过优化，可以利用选择性挂起。 （此功能要求供应商通过 Microsoft 操作系统描述符提供 INF 或支持。）

通过 USB 进行的最新 HID 更新还包括：

- 支持 USB 1.1、USB 2.0 和 USB 3.0。
- Windows 的所有客户端 Sku 上都提供了一个基于 USB 驱动程序的 HID，它包含在 WinPE 中。

## <a name="see-also"></a>另请参阅

- [HID USB 主页](https://www.usb.org/hid)
- [HID USB 规范](https://www.usb.org/sites/default/files/documents/hid1_11.pdf)
- [HID 使用情况表](https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf)
