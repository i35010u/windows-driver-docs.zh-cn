---
title: HID 传输概述
description: HID 传输概述
ms.assetid: E442CB87-992B-475A-A97F-9C22468BA877
keywords:
- HID 传输
- USB 传输
- 蓝牙传输
- 蓝牙
- 蓝牙 LE
- I2C
- 传输微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc7dcd173b88e1af43462e8ee01ba116a82c890
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565587"
---
# <a name="hid-transport-overview"></a>HID 传输概述


当前版本的 Windows 和以前版本的 Windows 支持 HID 传输。

| “传输”    | 内置微型驱动程序 | Version               |  说明 |
| ------------ | ----------------- | --------------------- | ---------- | 
| USB          | Hidusb        | Windows 7 及更高版本。  | Windows 操作系统2000可追溯上提供了对 USB HID 1.11 + 的支持。       |
| 蓝牙    | Hidbth        | Windows 7 及更高版本。  | Windows 操作系统可追溯上提供对蓝牙 HID 1.1 + 的支持。 |
| 蓝牙 LE | HidBthLE      | Windows 8 及更高版本。  | Windows 8 引入了对基于蓝牙 LE 的 HID 的支持。                                               |
| I I2C          | Hidi2c        | Windows 8 及更高版本。  | Windows 8 通过 I2C 引入了对 HID 的支持。                                                        |
| GPIO         | Hidinterrupt  | Windows 10 及更高版本。 | Windows 10 引入了对常规用途 i/o (GPIO) 按钮的支持。                         |

 

Microsoft 建议尽可能将内置驱动程序用于上表中列出的传输。

如果你的设备需要除 USB、Bluetooth、Bluetooth LE 或 I u 之外的其他传输, 你可以开发一个微型端口驱动程序, 该驱动程序将在[传输微型驱动程序](transport-minidrivers.md)主题中介绍。

## <a name="hid-transport-limits"></a>HID 传输限制


-   **报表描述符长度**

    传输微型驱动程序将报表描述符提交到[**HID\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidport/ns-hidport-_hid_descriptor)结构中的 Hidclass。 无论传输协议定义的大小如何传输 HID 报表描述符及其设备, 在 Hidclass 与 HID 微型驱动程序之间进行通信时, 实际的报表描述符大小都将受到限制。

-   **报表描述符中的 TLCs**

    Hidclass/Hidparse 驱动程序对可识别报表描述符中的 TLCs 数。 HID 微型端口驱动程序不知道该信息。 每个 TLC 至少有2个字节用于启动集合, 1 个字节用于结束集合。

-   **输入/输出/功能报表长度**

    Hidclass/Hidparse 驱动程序对定义 HID 输入、输出和功能报表的长度。 限制为 8 KB (减1位)。 即使对于报表, HID 微型驱动程序可以请求传输超过 8 KB, 也只会成功传输小于 8 KB 的报表。

| 内置微型驱动程序 | 报表描述符长度 | 在一个报表描述符中 TLCs | 输入/输出/功能报表长度 |
| ----------------- | ------------------------ | ----------------------------- | ---------------------------------- |
| Hidclass/Hidparse | 65535字节              | 21845                         | 8 KB-1 位                       |
| Hidusb            | 65535字节              | 不可用                           | 64 KB                              |
| Hidbth            | 65535字节              | 不可用                           | 64 KB                              |
| HidBthLE          | 65535字节              | 不可用                           | 64 KB                              |
| Hidi2c            | 65535字节              | 不可用                           | 64 KB                              |

 

 

 




