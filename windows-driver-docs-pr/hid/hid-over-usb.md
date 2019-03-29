---
title: 基于 USB 的 HID
description: USB 是 Windows 操作系统中支持的第一个 HID 传输。
ms.assetid: F892C910-BA33-4795-A803-9D3FD55782BC
keywords:
- HID 微型端口驱动程序
- USB
- USB 1.1
- USB 2.0
- USB 3.0
- USB、 HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9bcebf453540dceeb8d32217a17490373dbbf20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563983"
---
# <a name="hid-over-usb"></a>基于 USB 的 HID


USB 是 Windows 操作系统中支持的第一个 HID 传输。 相应的收件箱驱动程序在 Windows 2000 中引入，并且已从那时起所有操作系统中可用。

Windows 8 仍支持通过 USB HID 和已经过增强，包括从触摸板和键盘到传感器和供应商特定的设备类型的 HID 设备的新类。

HID over USB 还优化为利用的选择性挂起。 （此功能要求的供应商提供的 INF 或通过 Microsoft 操作系统描述符的支持。）

此外包括通过 USB 的 HID 到新的更新：

-   对 USB 1.1，USB 2.0 和 USB 3.0 支持。
-   HID USB 驱动程序通过可在所有客户端 Sku 的 Windows 上，并且包含在 WinPE 中。

 

 




