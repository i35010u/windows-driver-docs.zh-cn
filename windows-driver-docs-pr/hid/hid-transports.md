---
title: HID 传输方式
description: HID 传输方式
ms.assetid: E442CB87-992B-475A-A97F-9C22468BA877
keywords:
- HID 传输方式
- USB 传输
- 蓝牙传输
- 蓝牙
- 蓝牙 LE
- I2C
- 传输微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83f89c9240993851680fa20d755447edbc3b0a00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541895"
---
# <a name="hid-transports"></a>HID 传输方式


在当前和以前版本的 Windows 中受支持的 HID 传输方式。

| “传输”    | 在框微型驱动程序 | 版本               |  注释 |
| ------------ | ----------------- | --------------------- | ---------- | 
| USB          | Hidusb.sys        | Windows 7 及更高版本。  | 追溯到 Windows 2000 的 Windows 操作系统上提供的 USB HID 1.11 + 的支持。       |
| 蓝牙    | Hidbth.sys        | Windows 7 及更高版本。  | 追溯到 Windows Vista 的 Windows 操作系统上提供对蓝牙 HID 1.1 + 的支持。 |
| 蓝牙 LE | HidBthLE.dll      | Windows 8 及更高版本。  | Windows 8 引入了通过蓝牙 LE 的 HID 支持。                                               |
| I²C          | Hidi2c.sys        | Windows 8 及更高版本。  | Windows 8 引入了通过 I2C 的 HID 支持。                                                        |
| GPIO         | Hidinterrupt.sys  | Windows 10 及更高版本。 | Windows Windows 10 引入了支持通用 I/O (GPIO) 按钮。                         |

 

Microsoft 建议，只要有可能，为上表中列出的传输使用现成驱动程序。

如果你的设备需要 USB、 蓝牙、 蓝牙 LE 或 I²C 以外的传输，可以开发的微型端口驱动程序中所述[传输微型驱动程序](transport-minidrivers.md)主题

## <a name="hid-transport-limits"></a>HID 的传输限制


-   **报表描述符长度**

    传输微型驱动程序提交到 Hidclass 中的报告描述符[ **HID\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539885)结构。 无论使用其设备将传输 HID 报表描述符的传输协议定义的大小，实际的报表描述符大小可以 Hidclass 和 hid 标准的微型驱动程序之间的通信过程被限制。

-   **在报表描述符 TLCs**

    Hidclass/Hidparse 驱动程序对可察觉 TLCs 报表描述符中的数。 HID 微型端口驱动程序不知道该信息。 每个 TLC 具有至少 2 个字节开始收集和 1 个字节结束集合。

-   **输入/输出/功能报表长度**

    Hidclass/Hidparse 驱动程序对定义的 HID 输入、 输出和功能的报表的长度。 限制为 8 KB （减去 1 的位）。 即使 HID 微型驱动程序可以请求报表的多个 8 KB 的传输，只有小于 8 KB 的报表已成功传输。

| 在框微型驱动程序 | 报表描述符长度 | 在一个报表描述符 TLCs | 输入/输出/功能报表长度 |
| ----------------- | ------------------------ | ----------------------------- | ---------------------------------- |
| Hidclass/Hidparse | 65535 个字节              | 21845                         | 8 KB-1 的位                       |
| Hidusb            | 65535 个字节              | 不适用                           | 64 KB                              |
| Hidbth            | 65535 个字节              | 不适用                           | 64 KB                              |
| HidBthLE          | 65535 个字节              | 不适用                           | 64 KB                              |
| Hidi2c            | 65535 个字节              | 不适用                           | 64 KB                              |

 

 

 




