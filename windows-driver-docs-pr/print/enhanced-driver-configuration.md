---
title: 增强的驱动程序配置
description: GPD 和 PPD 文件可以用于提供增强的驱动程序 v4 打印驱动程序的配置信息。
ms.assetid: B208C661-4D5B-467A-8451-4382453EC09A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faafea3dfbe1dbe85258807e26345432e3105b3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576336"
---
# <a name="enhanced-driver-configuration"></a>增强的驱动程序配置


GPD 和 PPD 文件可以用于提供增强的驱动程序 v4 打印驱动程序的配置信息。

V4 驱动程序模型所基于的打印驱动程序然后可以从使用 Bidi 的设备中检索这些 GPD 和 PPD 文件。 这允许设备使用了打印类驱动程序以支持更丰富的功能而无需额外下载从 Windows 更新设置。

默认情况下支持 Ws-print v1.1 的驱动程序支持此功能。 但是，TCP/IP 的设备和 WS-打印 v1.0 设备可能也支持此功能通过实现指定以下 Bidi 架构元素的双向扩展文件。

**架构路径： 用于读取 GPD/PPD 文件的架构部分**

**节名称：** DriverConfigFiles

**架构路径：**\\Printer.Configuration.DriverConfigFiles

**描述:** 此新部分以 Bidi 架构的将包含要查询的设备驱动程序配置数据，包括 GPD 和 PPD 说明文件的架构值。

适用于读取 GPD 文件扩展

**架构名称：** GPDFile

**架构路径：**\\Printer.Configuration.DriverConfigFiles:GPDFile

**节点类型：** 值

**数据类型：** BIDI\_字符串

**描述:** 设备的完整 GPD 文件。 这包含可用且最新按照该设备的当前设置的所有特定设备配置信息。

适用于读取 PPD 文件扩展

**架构名称：** PPDFile

**架构路径：**\\Printer.Configuration.DriverConfigFiles:PPDFile

**节点类型：** ReplTest1

**数据类型：** BIDI\_字符串

**描述:** 设备的完整 PPD 文件。 这包含可用且最新按照该设备的当前设置的所有特定设备配置信息。

**请注意**  USB 设备，无论你使用 GPD 或 PPD 文件中，Bidi 扩展 XML 文件必须指定 drvPrinterEvent 属性并设置其值为"true"。 这可确保 Bidi 缓存刷新刷新一次更新的元素。

 

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



