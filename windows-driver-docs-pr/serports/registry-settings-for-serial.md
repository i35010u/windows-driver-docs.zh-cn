---
title: 用于串行的注册表设置
description: 用于串行的注册表设置
ms.assetid: be64d9d7-6d6b-4430-96a3-ac071d48b121
keywords:
- 串行驱动程序 WDK、 注册表设置
- 注册表 WDK 串行设备
- 串行设备 WDK、 注册表设置
- 串行设备 WDK，串行驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa474b998814271090aad38f6c0a97fddc3b233
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575238"
---
# <a name="registry-settings-for-serial"></a>用于串行的注册表设置





本部分介绍以下序列使用配置的串行设备的注册表设置：

[串行服务的注册表设置](registry-settings-for-the-serial-service.md)

[Plug and Play 串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)

[传统 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)

序列使用的注册表设置来通过以下方式配置的串行设备：

-   如果存在特定于设备的条目值，则序列将使用它。

-   特定于设备的条目值不存在，但没有相应的串行服务条目值，如果序列使用的服务条目值。

-   如果没有特定于设备的条目值，并且没有相应的串行服务条目值，序列使用默认服务值中以静态方式定义的*serial.sys*。

 

 




