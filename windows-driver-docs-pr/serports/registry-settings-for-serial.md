---
title: 用于串行的注册表设置
description: 用于串行的注册表设置
keywords:
- 串行驱动程序 WDK，注册表设置
- 注册表 WDK 串行设备
- 串行设备 WDK，注册表设置
- 串行设备 WDK，串行驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81e64f0f303c9b1a164bfac25e5b3e0960ceb15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811987"
---
# <a name="registry-settings-for-serial"></a>用于串行的注册表设置





本部分介绍串行用于配置串行设备的以下注册表设置：

[用于串行服务的注册表设置](registry-settings-for-the-serial-service.md)

[用于即插即用串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)

[用于旧版 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)

串行使用注册表设置按以下方式配置串行设备：

-   如果存在特定于设备的条目值，则串行将使用它。

-   如果设备特定的条目值不存在，但有相应的串行服务条目值，则串行将使用服务条目值。

-   如果设备特定的条目值不存在并且没有相应的串行服务条目值，则串行将使用 *serial.sys* 中静态定义的默认服务值。

 

 




