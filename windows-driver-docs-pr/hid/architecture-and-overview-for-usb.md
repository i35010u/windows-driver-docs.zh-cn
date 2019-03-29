---
title: 通过 USB 传输的 hid 标准的体系结构
description: 本部分介绍用于通过 USB 传输支持 HID 设备的驱动程序堆栈。
ms.assetid: D0D87B86-AD36-442A-9D36-571D12A360D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d33f5f44205c2ba8b05f649dabd2b4f417be878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565892"
---
# <a name="architecture-and-overview"></a>体系结构和概述


本部分介绍用于通过 USB 传输支持 HID 设备的驱动程序堆栈。

USB 驱动程序堆栈上的 HID 由 Microsoft 提供的以下组件组成。 下图描绘了堆栈和以下组件。

![hid usb 驱动程序体系结构 ](images/transport-usb.png)

Windows 8 提供了实现通过 USB HID 协议规范的版本 1.1 + WDF 基于 HID 微型端口驱动程序。 此驱动程序名为 HIDUSB。SYS。 Windows 将加载此驱动程序基于 USB 设备类兼容 ID 匹配项。

 

 




