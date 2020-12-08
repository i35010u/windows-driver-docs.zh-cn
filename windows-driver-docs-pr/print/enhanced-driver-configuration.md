---
title: 增强的驱动程序配置
description: 可以使用 GPD 和 PPD 文件为 v4 打印驱动程序提供增强的驱动程序配置信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806b80559c744e43bfdebce7725fdfc869360796
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797127"
---
# <a name="enhanced-driver-configuration"></a>增强的驱动程序配置


可以使用 GPD 和 PPD 文件为 v4 打印驱动程序提供增强的驱动程序配置信息。

然后，基于 v4 驱动程序模型的打印驱动程序可以使用双向从设备检索这些 GPD 和 PPD 文件。 这允许使用打印类驱动程序的设备支持更丰富的功能集，而无需 Windows 更新的其他下载。

默认情况下，支持 WS-Print v1.1 的驱动程序支持此功能。 但是，TCP/IP 设备和 WS-Print v1.0 设备还可以通过实现指定以下双向架构元素的双向扩展文件来支持此功能。

**架构路径：用于读取 GPD/PPD 文件的架构部分**

**节名称：** DriverConfigFiles

**架构路径：** \\Printer.Configu。DriverConfigFiles

**说明：** 对于双向架构，此新部分将包含用于查询设备中的驱动程序配置数据的架构值，包括 GPD 和 PPD 说明文件。

用于读取 GPD 文件的扩展

**架构名称：** GPDFile

**架构路径：** \\Printer.Configu。DriverConfigFiles:GPDFile

**节点类型：** 负值

**数据类型：** 双向 \_ 字符串

**说明：** 设备的完整 GPD 文件。 这包含所有可用的特定设备配置信息，并根据设备的当前设置更新为最新。

用于读取 PPD 文件的扩展

**架构名称：** PPDFile

**架构路径：** \\Printer.Configu。DriverConfigFiles:PPDFile

**节点类型：** 负值

**数据类型：** 双向 \_ 字符串

**说明：** 设备的完整 PPD 文件。 这包含所有可用的特定设备配置信息，并根据设备的当前设置更新为最新。

**注意**  对于 USB 设备，无论是使用 GPD 还是 PPD 文件，双向扩展 XML 文件都必须指定 drvPrinterEvent 属性，并将其值设置为 "true"。 这可确保在双向缓存刷新后更新元素。

 

以下 XML 片段演示了使用 drvPrinterEvent 属性的正确语法：

```xml
<?xml version='1.0'?>
...
  <Property name='DeviceInfo'>
     <Const name="Category" type="BIDI_STRING" value="DeviceCategory"/> 
     <Value name="QueueProperty" type="BIDI_STRING" accessType="Get" queryKey="Configuration" refreshInterval="60" drvPrinterEvent="true"/> 
  </Property> 
...
```

## <a name="related-topics"></a>相关主题

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)  



