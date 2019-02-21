---
title: PNPCPU 典型会话
description: PNPCPU 典型会话
ms.assetid: d0c1b6aa-fe23-4d01-aecf-897aba3672c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b385dd4a84415d30c9178e0f88a62548ed63067a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544862"
---
# <a name="pnpcpu-typical-session"></a>PNPCPU 典型会话


在运行时 **-安装**命令，PNPCPU 执行以下操作：

-   安装总线枚举器驱动程序。

-   将标记显示问题代码 28-设备管理器中可见的所有现有处理器。

-   将 ONECPU 添加到引导配置数据 (BCD) 设置。

-   Windows 正在使用时保存的处理器数 **-安装**运行。

-   预安装的处理器驱动程序的 INF 文件。

在安装完成后，将看到以下消息：

```
Enabled hot add cpu...
Please reboot the system before proceeding with the test
```

重新启动系统通过执行关闭，从命令行中，或从系统菜单选项。

重新启动计算机后，Windows 将仅使用一个逻辑处理器。 您可以通过查找具有错误代码 28 处理器确认这在设备管理器。

 

 





