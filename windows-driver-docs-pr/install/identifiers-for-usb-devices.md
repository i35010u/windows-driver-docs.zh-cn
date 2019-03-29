---
title: USB 设备的标识符
description: USB 设备的标识符
ms.assetid: 9597eae3-2aaf-4942-9d03-1b03bd12fcfd
keywords:
- 设备标识字符串 WDK、 USB 设备
- 标识字符串 WDK 设备、 USB 设备
- 标识符 WDK 设备、 USB 设备
- USB 标识符 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46f092c8d3fcda890f0e14e3c97934dbff07e275
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562094"
---
# <a name="identifiers-for-usb-devices"></a>USB 设备的标识符





本部分介绍设备、 硬件和生成的 USB 设备兼容的标识符。

Windows 操作系统会生成适用于打印机和大容量存储设备的特殊 USB 标识符，因为以下文档将 USB 标识符划分为两个组：

[标准 USB 标识符](standard-usb-identifiers.md)

[特殊的 USB 标识符](special-usb-identifiers.md)

对于所有 USB 设备，USB 总线驱动程序将生成一组标准的标识符组成的 USB 设备和接口描述符从检索的值。 在上述的两个部分的第一个讨论了标准 USB 标识符。 除了标准的 USB 标识符，大容量存储和打印机设备的本机 Windows 驱动程序生成一组单独的 USB 标识符组成与打印机和存储设备的特殊相关性有关的信息。 第二个节中讨论这些特殊的 USB 标识符。

**请注意**  从 Microsoft Windows 2000 开始，USB 标识符中嵌入的数字是以十六进制格式。

 

 

 





