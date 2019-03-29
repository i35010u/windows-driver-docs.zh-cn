---
title: HardDisk
description: HardDisk
ms.assetid: 88eadea0-54cb-4c19-90d2-9941b13b9303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aff1b423946c6011954835c32aa4e1f8e83f56e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562148"
---
# <a name="harddisk"></a>HardDisk


架构路径：\\Printer.Configuration.HardDisk

节点类型： 属性

说明： 安装在设备硬盘值项。

硬盘属性包含三个对子值：安装容量和可用空间。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 安装

架构路径：\\Printer.Configuration.HardDisk:Installed

节点类型： 值

数据类型： BIDI\_BOOL

说明： 指示是否在设备上安装硬盘。 如果 **，则返回 TRUE**，安装硬盘; 如果**FALSE**，未安装硬盘。

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

架构路径：\\Printer.Configuration.HardDisk:Capacity

节点类型： 值

数据类型： BIDI\_INT

说明： 的容量，以兆字节 (MB) 的已安装硬盘。

### <a name="span-idfreespacespanspan-idfreespacespan-freespace"></a><span id="freespace"></span><span id="FREESPACE"></span> FreeSpace

架构路径：\\Printer.Configuration.HardDisk:FreeSpace

节点类型： 值

数据类型： BIDI\_INT

说明： 当前可用的已安装硬盘可用空间，以兆字节 (MB)。

 

 




