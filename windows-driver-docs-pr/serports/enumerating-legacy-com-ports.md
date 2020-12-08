---
title: 枚举旧版 COM 端口
description: 枚举旧版 COM 端口
keywords:
- 串行驱动程序 WDK，COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
- 枚举 COM 端口 WDK 串行设备
- 旧 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9fe380b5d972eca697a0cf201b96b57811b811
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812035"
---
# <a name="enumerating-legacy-com-ports"></a>枚举旧版 COM 端口





串行函数驱动程序当前枚举在注册表中指定的旧 [COM 端口](configuration-of-com-ports.md) 。 串行枚举的大多数 COM 端口都是无微控制器的多端口板上的传统设备。 请注意，此枚举函数将从串行中删除，并在将来的版本中作为安装程序的一部分包含。

串行执行以下步骤：

1.  检查驱动程序服务注册表项下由子项标识的 COM 端口 **。 \\Services \\ 串行 \\ 参数** \\ &lt; *设备子项 &gt; 。*

    对于每个设备子项，串行获取 [旧 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)中所述的注册表信息。

2.  检查 COM 端口是否为旧设备。 如果 **PnPDeviceID** 条目的值为 null，则设备为旧设备。 如果 COM 端口是旧设备，则 "仅串行" 执行剩余步骤。  (如果 **PnPDeviceID** 为非空，则该端口是其总线驱动程序所枚举的即插即用设备。 ) 

3.  如果 COM 端口是旧设备，则串行确定它是否已检测到它。

    串行使用 COM 端口的 **LegacyDiscovered** 入口值 (REG \_ DWORD) 。 如果 **LegacyDiscovered** 为非零，则串行先前检测到端口，并跳过再次枚举。 即插即用管理器添加并启动旧版端口。

    如果 **LegacyDiscovered** 为零，则串行先前未检测到端口，并向即插即用 MANAGER 报告 COM 端口。 即插即用管理器返回 PDO，并在其设备树中为 COM 端口创建一个条目。

4.  为每个检测到的旧 COM 端口创建 FDO，并将其附加到设备堆栈。

5.  在旧 COM 端口的即插即用注册表项下设置 COM 端口信息。

    串行使用从注册表中读取的旧 COM 端口信息的子集。 有关详细信息，请参阅 [即插即用串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。

6.  启动旧 COM 端口。

 

 




