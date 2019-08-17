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
- USB, HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff088091329327f6063bba24c7f9c92d4827661b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565576"
---
# <a name="hid-over-usb-overview"></a>基于 USB 的 HID 概述


USB 是 Windows 操作系统中第一个受支持的 HID 传输。 Windows 2000 中引入了相应的收件箱驱动程序, 并且自那时起已在所有操作系统中提供。

Windows 8 在 USB 上继续支持 HID, 并已进行了增强, 包括触摸板和键盘到传感器和供应商特定设备类型的新类。

USB 上的 HID 还经过优化, 可以利用选择性挂起。 (此功能要求供应商通过 Microsoft 操作系统描述符提供 INF 或支持。)

通过 USB 进行的最新 HID 更新还包括:

-   支持 USB 1.1、USB 2.0 和 USB 3.0。
-   Windows 的所有客户端 Sku 上都提供了一个基于 USB 驱动程序的 HID, 它包含在 WinPE 中。

 

 




