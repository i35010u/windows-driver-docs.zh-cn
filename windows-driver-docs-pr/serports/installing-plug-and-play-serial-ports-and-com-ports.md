---
title: 安装即插串行端口和 COM 端口
description: 安装即插串行端口和 COM 端口
ms.assetid: 48a489a1-6ed9-4e17-a7b5-0f2325486ab6
keywords:
- 串行驱动程序 WDK，插设备
- 即插即用串行设备 WDK
- 串行设备 WDK，插
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54ad46994756effe287f65ea4ac87802511a8ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544099"
---
# <a name="installing-plug-and-play-serial-ports-and-com-ports"></a>安装即插串行端口和 COM 端口





默认情况下，端口类安装程序和串行函数驱动程序的组合的操作作为 COM 端口配置的串行端口。 如果序列创建的串行端口的 COM 端口设备接口**SerialSkipExternalNaming**条目值，设备不存在或设置为零。 有关序列创建的 COM 端口的 COM 端口设备接口的方式以及如何重写此操作的详细信息，请参阅[外部命名的 COM 端口](external-naming-of-com-ports.md)。

在安装的串行端口，端口类安装程序将执行以下任务：

1. 选择 COM 端口号，并设置端口名称**PortName**条目下设备的硬件密钥的值。 端口名称采用格式 COM<em>&lt;n&gt;</em>，其中*&lt;n&gt;* 是端口号。 如果序列创建的串行端口的 COM 端口接口时，序列将使用的值**PortName**作为 COM 端口的符号链接名称。

2. 显示默认属性页对话框中，这样用户就可以选择的端口设置。 有关如何安装自定义属性页的信息，请参阅[安装 COM 端口的高级属性页](installing-an-advanced-properties-page-for-a-com-port.md)。

3. 设置设备的设备友好名称。 获取名称使用 SPDRP\_FRIENDLYNAME 标志**SetupDiGetDeviceRegistryProperty**。

你可以提供设置的共同安装程序[插串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。 如果不存在注册表中条目值，序列将使用默认值为端口。

 

 




