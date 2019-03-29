---
title: 创建 INF 文件
description: 创建 INF 文件
ms.assetid: c45fb42c-f0d6-4ab8-9a19-4bbf98c4cf8c
keywords:
- 游戏杆 WDK HID，INF 文件
- 虚拟游戏杆驱动程序 WDK HID，INF 文件
- VJoyD WDK HID，INF 文件
- INF 文件 WDK 游戏杆
- INF 文件 WDK 游戏杆创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 295fbf690cfbc271105a04fe09c7fd38d9a564ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568298"
---
# <a name="creating-an-inf-file"></a>创建 INF 文件





使用 INF 文件以提供对系统的所有必要信息应安装所有微型驱动程序和 OEM 定义游戏杆。 INF 文件描述的设备安装方面的设备，需要复制的文件、 任何兼容的设备，设备要求，并更改为注册表的所有系统资源类。 不需要自定义标准的模拟驱动程序的 INF 文件来复制任何文件、 状态兼容的设备，或者指定系统资源。 INF 文件可以指定其他操作，例如，修改 Autoexec.bat 文件中，但这不是通常所需游戏杆微型驱动程序。

INF 文件包含以下主题中描述的元素：

[设置设备类](setting-the-device-class.md)

[选择源文件](selecting-source-files.md)

[设置特定于制造商的数据](setting-the-manufacturer-specific-data.md)

[设置 LogConfig 条目](setting-up-logconfig-entries.md)

[设置 AddReg 条目](setting-up-addreg-entries.md)

 

 




