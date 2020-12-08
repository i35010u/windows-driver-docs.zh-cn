---
title: 通过 USB 传输的 HID 体系结构
description: 本部分介绍支持通过 USB 传输的 HID 的设备的驱动程序堆栈。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf7b4e07a2fb5ca7d5170c4db874e7a29fa26a95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791549"
---
# <a name="architecture-and-overview"></a>体系结构和概述


本部分介绍通过 USB 传输支持 HID 的设备的驱动程序堆栈。

基于 USB 驱动程序的 HID 堆栈包含 Microsoft 提供的下列组件。 下图描绘了堆栈和这些组件。

![hid-usb 驱动程序体系结构 ](images/transport-usb.png)

Windows 8 提供了一个基于 WDF 的 HID 微型端口驱动程序，该驱动程序实现了基于 USB 的 HID 协议规范的版本 1.1 +。 此驱动程序名为 HIDUSB.SYS。 Windows 基于与 USB 设备类兼容的 ID 匹配加载此驱动程序。

 

 




