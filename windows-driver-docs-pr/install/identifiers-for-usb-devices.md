---
title: USB 设备的标识符
description: USB 设备的标识符
keywords:
- 设备标识字符串 WDK，USB 设备
- 标识字符串 WDK 设备，USB 设备
- 标识符 WDK 设备，USB 设备
- USB 标识符 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 879166814ddeb42eac75ae3cc46619277dba3e38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791735"
---
# <a name="identifiers-for-usb-devices"></a>USB 设备的标识符





本部分介绍 USB 设备生成的设备、硬件和兼容的标识符。

由于 Windows 操作系统为打印机和大容量存储设备生成了特殊的 USB 标识符，以下文档将 USB 标识符分成两组：

[标准 USB 标识符](standard-usb-identifiers.md)

[特殊 USB 标识符](identifiers-generated-by-usbstor-sys.md)

对于所有 USB 设备，USB 总线驱动程序会生成一组标准的标识符，由从 USB 设备和接口描述符检索的值组成。 上面所示的两个部分中的第一个部分讨论了标准 USB 标识符。 除了标准 USB 标识符以外，用于大容量存储和打印机设备的本机 Windows 驱动程序还会生成一组单独的 USB 标识符，这些标识符由与打印机和存储设备的特殊相关性相关的信息组成。 在第二部分中讨论了这些特殊的 USB 标识符。

**注意**  从 Microsoft Windows 2000 开始，嵌入 USB 标识符中的数字是十六进制格式。

 

 

 





