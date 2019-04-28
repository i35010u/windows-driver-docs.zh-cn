---
title: 枚举旧版 COM 端口
description: 枚举旧版 COM 端口
ms.assetid: 36a73153-0e3e-4b41-9b3d-08b29b5220fe
keywords:
- 串行驱动程序 WDK、 COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
- 枚举 COM 端口 WDK 串行设备
- 传统的 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355d59ab334d70715131ab2605ae39b2b46def07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341294"
---
# <a name="enumerating-legacy-com-ports"></a>枚举旧版 COM 端口





串行函数驱动程序当前枚举旧[COM 端口](configuration-of-com-ports.md)在注册表中指定的。 大多数序列枚举的 COM 端口是没有微控制器的多端口板上的旧设备。 请注意，将从序列中删除，安装程序的未来版本中的一部分包含此枚举函数。

序列将执行以下步骤：

1.  检查由驱动程序服务注册表项下的子项标识 COM 端口 **...\\Services\\串行\\参数**\\&lt;*设备子项&gt;。*

    每个设备的子项，序列获取注册表信息中所述[传统 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)。

2.  检查 COM 端口是否旧设备。 如果**PnPDeviceID**条目值为 null，则该设备是旧的设备。 如果 COM 端口是旧的设备，序列仅执行剩余步骤。 (如果**PnPDeviceID**为非 null，端口是插设备枚举其总线驱动程序。)

3.  如果 COM 端口是旧的设备，序列确定如果它以前检测到它。

    序列使用的 COM 端口**LegacyDiscovered**条目值 (REG\_DWORD)。 如果**LegacyDiscovered**为非零值，序列以前检测到的端口和跳过再次枚举。 插管理器将添加并启动旧的端口。

    如果**LegacyDiscovered**为零，序列没有以前检测到的端口和插管理器报告 COM 端口。 插管理器返回 PDO，并在其设备树中创建的 COM 端口的条目。

4.  创建每个检测到旧的 COM 端口 FDO 并将其附加到设备堆栈。

5.  设置旧的 COM 端口插注册表项下的 COM 端口信息。

    序列使用从注册表中读取为传统的 COM 端口的信息的子集。 有关详细信息，请参阅[即插即用和播放串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。

6.  启动传统的 COM 端口。

 

 




