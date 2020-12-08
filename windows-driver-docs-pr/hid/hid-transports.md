---
title: HID 传输概述
description: HID 传输概述
keywords:
- HID 传输
- USB 传输
- 蓝牙传输
- 蓝牙
- 蓝牙 LE
- I2C
- 传输微型驱动程序
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: a20165c66fe592f35a5bf1770468ca5a5a03f57f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838615"
---
# <a name="hid-transport-overview"></a>HID 传输概述

## <a name="hid-transports-supported-in-windows"></a>Windows 中支持的 HID 传输

| Transport    | 内置微型驱动程序 | 版本               |  说明 |
| ------------ | ----------------- | --------------------- | ---------- | 
| USB          | Hidusb.sys        | Windows 7 及更高版本。  | Windows 操作系统2000可追溯上提供了对 USB HID 1.11 + 的支持。       |
| 蓝牙    | Hidbth.sys        | Windows 7 及更高版本。  | Windows 操作系统可追溯上提供对蓝牙 HID 1.1 + 的支持。 |
| 蓝牙 LE | HidBthLE.dll      | Windows 8 和更高版本。  | Windows 8 引入了对基于蓝牙 LE 的 HID 的支持。                                               |
| I i2c          | Hidi2c.sys        | Windows 8 和更高版本。  | Windows 8 通过 I2C 引入了对 HID 的支持。                                                        |
| GPIO         | Hidinterrupt.sys  | Windows 10 及更高版本。 | Windows 10 中引入了对常规用途 i/o (GPIO) 按钮的支持。                         |

Microsoft 建议对上表中列出的传输使用附带的驱动程序。

如果设备要求除 USB、Bluetooth、Bluetooth LE 或 I u 之外的其他传输，则建议使用 [传输微型驱动程序](transport-minidrivers.md) 中所述的小型端口驱动程序。

## <a name="hid-transport-limits"></a>HID 传输限制

- **报表描述符长度**

    传输微型驱动程序将报表描述符提交到 [**HID \_ 描述符**](/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_descriptor) 结构中的 Hidclass。 无论传输协议定义的大小如何传输 HID 报表描述符及其设备，在 Hidclass 与 HID 微型驱动程序之间进行通信时，实际的报表描述符大小都将受到限制。

- **报表描述符中的 TLCs**

    Hidclass/Hidparse 驱动程序对可识别报表描述符中的 TLCs 数。 HID 微型端口驱动程序没有该信息。 每个 TLC 至少有2个字节用于启动集合，1个字节用于结束集合。

- **输入/输出/功能报表长度**

    Hidclass/Hidparse 驱动程序对定义 HID 输入、输出和功能报表的长度。 此限制为 8 KB (减1位) 。 即使对于报表，HID 微型驱动程序可以请求传输超过 8 KB，也只会成功传输小于 8 KB 的报表。

| 内置微型驱动程序 | 报表描述符长度 | 在一个报表描述符中 TLCs | 输入/输出/功能报表长度 |
| ----------------- | ------------------------ | ----------------------------- | ---------------------------------- |
| Hidclass/Hidparse | 65535字节              | 21845                         | 8 KB-1 位                       |
| Hidusb            | 65535字节              | 空值                           | 64 KB                              |
| Hidbth            | 65535字节              | 空值                           | 64 KB                              |
| HidBthLE          | 65535字节              | 空值                           | 64 KB                              |
| Hidi2c            | 65535字节              | 空值                           | 64 KB                              |

## <a name="see-also"></a>另请参阅

Windows 硬件实验室工具包中的[USB 一般 HID 测试](/windows-hardware/test/hlk/testref/f7949ab5-dd13-4c74-876f-6d54ff85e213) (的 HLK) 包含 HidUsb 和 HidClass 驱动程序。 没有适用于第三方 HID 小型驱动程序的 HLK 测试。
