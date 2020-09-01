---
title: 安装旧版 COM 端口
description: 安装旧版 COM 端口
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- 旧 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 821738dd2afabf813ea4d3d4e91f84540e293f3b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187113"
---
# <a name="installing-legacy-com-ports"></a>安装旧版 COM 端口

串行函数驱动程序始终将旧版串行端口配置为 [COM 端口](configuration-of-com-ports.md)。

串行通过读取 **中 \\ 的相应 COM 端口子项来检测旧端口是否存在。Services \\ 串行 \\ 参数** 密钥。 若要安装旧的 COM 端口，必须在此项下为设备设置一个旧版 COM 端口子项。 COM 端口子项包含 [旧 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)。

如果已加载串行，它会通过检查旧端口的 **LegacyDiscovered** 条目值来确定以前未检测到的旧版端口。 如果此项值不存在或为零，则串行执行以下任务：

1. 调用 [**IoReportDetectedDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice) 将设备报告给即插即用管理器。

2. 将端口的 **LegacyDiscovered** 输入值设置为0x00000001，这表示端口已报告。

3. 将 COM 端口子项下的一些条目值复制到**IoReportDetectedDevice**返回的物理设备对象 (*PDO*) 即插即用设备密钥。

4. 串行将即插即用设备密钥下的 **portvalue** 条目值设置为旧 COM 端口子项下 **DosDevices** 条目值的值。 对于序列复制的所有其他输入值，它会保留相同的条目值名称。 有关串行复制的入口值的详细信息，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中提供的串行示例代码。

**IoReportDetectedDevice**调用将端口标记为根枚举设备。 在后续系统启动时，即插即用管理器会根据其 INF 文件中的信息自动配置设备。

即插即用 manager 为旧 COM 端口创建以下 [兼容 id](../install/compatible-ids.md) ： DETECTEDInternal \\ SERIAL 和检测到的 \\ 串行。