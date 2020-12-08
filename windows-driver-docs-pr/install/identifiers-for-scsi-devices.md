---
title: SCSI 设备的标识符
description: SCSI 设备的标识符
keywords:
- 设备标识字符串 WDK，SCSI 设备
- 标识字符串 WDK 设备，SCSI 设备
- 标识符 WDK 设备，SCSI 设备
- SCSI 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 09/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: bbff2100312ee471bd57e404c698584781575413
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829915"
---
# <a name="identifiers-for-scsi-devices"></a>SCSI 设备的标识符

从 Windows 10 版本2004开始，版本 (OS 版本19041.488 或更高版本) ，可用于支持 [STOR_RICH_DEVICE_DESCRIPTION](/windows-hardware/drivers/ddi/storport/ns-storport-_stor_rich_device_description) 结构的 NVMe 存储磁盘驱动器的其他两个标识符：

`SCSI\t*v(8)p(40)`

其中：

- t * 是可变长度的设备类型代码

- v (8) 是8个字符的供应商标识符

- p (40) 是40字符产品标识符

`SCSI\t*v(8)p(40)r(8)`

其中：

- t * 是可变长度的设备类型代码

- v (8) 是8个字符的供应商标识符

- p (40) 是40字符产品标识符

- r (8) 是8个字符的修订级别值

在 Windows 10 之前的 Windows 版本中，版本 2004 (OS 版本19041.488 或更高版本) 中， (SCSI) 设备的小型计算机系统接口的设备 ID 格式如下所示：

`SCSI\\t\*v(8)p(16)r(4)`

其中：

- *t \** 是可变长度的设备类型代码

- *v (8)* 是8个字符的供应商标识符

- *p (16)* 是16个字符的产品标识符

- *r (4)* 为4个字符的修订级别值

总线枚举器通过对内部字符串表进行索引来确定设备类型，方法是使用通过查询设备获取的数字编码的 SCSI 设备类型代码，如下表所示。 其余组件只是由设备返回的字符串，但带有特殊字符 (包括空格、逗号和任何以下划线替换的非打印图形) 。

SCSI 端口驱动程序当前返回以下设备类型字符串，这是对应于标准 SCSI 类型代码的前九个字符串。

| SCSI 类型代码 | 设备类型 | 泛型类型 | 外围设备 ID |
|--|--|--|--|
| DIRECT_ACCESS_DEVICE (0)  | 磁盘 | GenDisk | DiskPeripheral |
| SEQUENTIAL_ACCESS_DEVICE (1)  | 顺序程序 |  | TapePeripheral |
| PRINTER_DEVICE (2)  | 打印机 | GenPrinter | PrinterPeripheral |
| PROCESSOR_DEVICE (3)  | 处理器 |  | OtherPeripheral |
| WRITE_ONCE_READ_MULTIPLE_DEVICE (4)  | 蠕虫 | GenWorm | WormPeripheral |
| READ_ONLY_DIRECT_ACCESS_DEVICE (5)  | 光盘 | GenCdRom | CdRomPeripheral |
| SCANNER_DEVICE (6)  | 扫描仪 | GenScanner | ScannerPeripheral |
| OPTICAL_DEVICE (7)  | 可选 | GenOptical | OpticalDiskPeripheral |
| MEDIUM_CHANGER (8)  | 转换器 | ScsiChanger | MediumChangerPeripheral |
| COMMUNICATION_DEVICE (9)  | Net | ScsiNet | CommunicationsPeripheral |
| 10 | ASCIT8 | ScsiASCIT8 | ASCPrePressGraphicsPeripheral |
| 11 | ASCIT8 | ScsiASCIT8 | ASCPrePressGraphicsPeripheral |
| 12 | Array | ScsiArray | ArrayPeripheral |
| 13 | 机箱 | ScsiEnclosure | EnclosurePeripheral |
| 14 | 红细胞 | ScsiRBC | RBCPeripheral |
| 15 | CardReader | ScsiCardReader | CardReaderPeripheral |
| 16 | 网桥 | ScsiBridge | BridgePeripheral |
| 17 | 其他 | ScsiOther | OtherPeripheral |

磁盘驱动器的设备 ID 的示例如下所示：

`SCSI\\DiskSEAGATE_ST39102LW_______0004`

除了设备 ID 之外，还存在四个硬件 Id：

`SCSI\\t\*v(8)p(16)`

`SCSI\\t\*v(8)`

`SCSI\\v(8)p(16)r(1)`

`V(8)p(16)r(1)`

在这些附加标识符的第三个和第四个中， *r (1)* 只表示修订标识符的第一个字符。 以下示例演示了这些硬件 Id：

`SCSI\\DiskSEAGATE_ST39102LW_______`

`SCSI\\DiskSEAGATE_`

`SCSI\\DiskSEAGATE_ST39102LW_______0`

`SEAGATE_ST39102LW_______0`

SCSI 端口驱动程序只提供一个兼容 ID，即上表中一个可变大小的泛型类型代码之一。

例如，磁盘驱动器的兼容 ID 如下：

`GenDisk`

除了 SCSI 驱动程序的 SCSI 驱动程序外，scsi 驱动程序的 INF 文件中使用的一般标识符都是通用的。

请注意，SCSI 端口驱动程序不会为顺序访问和 "处理器" 设备返回通用名称。
