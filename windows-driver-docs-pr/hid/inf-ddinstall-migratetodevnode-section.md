---
title: INF DDInstall.MigrateToDevNode 节
description: INF DDInstall.MigrateToDevNode 节
ms.assetid: a4edbc9e-a2d0-4012-aca9-0b357939a881
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- DDInstall.MigrateToDevNode 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60af77d117b1b7c9c21923a982da6f25cef7be9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364679"
---
# <a name="inf-ddinstallmigratetodevnode-section"></a>INF DDInstall.MigrateToDevNode 节





**\[**<em>安装的部分名称</em>**。MigrateToDevNode\]** |
**\[**<em>安装部分名称</em>**.nt。MigrateToDevNode\]** |
**\[**<em>安装部分名称</em>**.ntx86。MigrateToDevNode\]** |
**\[**<em>安装部分名称</em>**.ntia64。MigrateToDevNode\]**

<em>ServiceName</em>**=**<em>value-name</em>\[**,**<em>value-name</em>\],...键盘和鼠标类安装程序将复制的项值的列表指定的*值名称*注册表项中的字符串**HKLM\\系统\\CurrentControlSet\\服务\\**<em>ServiceName</em>**\\参数**到要安装的设备的设备节点。

### <a name="entries-and-values"></a>条目和值

<a href="" id="servicename"></a>*ServiceName*  
指定与设备端口相关联的服务名称 (例如， **i8042prt**， **sermouse**，依此类推)。

<a href="" id="value-name"></a>*value-name*  
指定注册表项下的项值**HKLM\\系统\\CurrentControlSet\\Services\\**<em>ServiceName</em> **\\参数**。

### <a href="" id="comments"></a>备注

Microsoft 支持 INF <em>DDinstall</em>**。MigratetoDevNode**部分主要是为了便于移植 Windows NT 4.0 旧设备为 Windows 2000 及更高版本。

键盘和鼠标类安装程序将所有复制*值名称*条目值之前在系统启动设备堆栈。 指定的项值可以是任何有效的注册表条目的值。 *值名称*条目的值不会从删除 **...\\**  <em>ServiceName</em>**\\参数**注册表项。

 

 




