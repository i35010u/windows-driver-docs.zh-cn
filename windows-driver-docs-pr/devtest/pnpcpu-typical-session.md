---
title: PNPCPU 典型会话
description: PNPCPU 典型会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a57f481d1b5e74f75eeaa02d35e4622968e073
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841041"
---
# <a name="pnpcpu-typical-session"></a>PNPCPU 典型会话


运行 **-install** 命令时，PNPCPU 会执行以下操作：

-   安装总线枚举器驱动程序。

-   用设备管理器中显示的问题代码28标记所有现有处理器。

-   将 ONECPU 添加到引导配置数据 (BCD) 设置。

-   在运行 **安装** 时，保存 Windows 正在使用的处理器数。

-   预先安装处理器驱动程序的 INF 文件。

安装完成后，你将看到以下消息：

```
Enabled hot add cpu...
Please reboot the system before proceeding with the test
```

通过从命令行或系统菜单选项执行关机来重新启动系统。

重新启动计算机后，Windows 将只使用一个逻辑处理器。 可以通过查找具有错误代码28的处理器，在设备管理器中确认这一点。

 

 





