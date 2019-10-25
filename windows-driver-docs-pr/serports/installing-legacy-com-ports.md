---
title: 安装旧版 COM 端口
description: 安装旧版 COM 端口
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- 旧 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4e01c1b32e488d678e3e2b4bb29f3ca2bed9ea3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842443"
---
# <a name="installing-legacy-com-ports"></a>安装旧版 COM 端口

串行函数驱动程序始终将旧版串行端口配置为[COM 端口](configuration-of-com-ports.md)。

串行通过读取 **\\Services\\串行\\参数**密钥下的相应 COM 端口子项，检测旧端口是否存在。 若要安装旧的 COM 端口，必须在此项下为设备设置一个旧版 COM 端口子项。 COM 端口子项包含[旧 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)。

如果已加载串行，它会通过检查旧端口的**LegacyDiscovered**条目值来确定以前未检测到的旧版端口。 如果此项值不存在或为零，则串行执行以下任务：

1. 调用[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)将设备报告给即插即用管理器。

2. 将端口的**LegacyDiscovered**输入值设置为0x00000001，这表示端口已报告。

3. 将 COM 端口子项下的一些条目值复制到**IoReportDetectedDevice**返回的物理设备对象（*PDO*）即插即用设备密钥。

4. 串行将即插即用设备密钥下的**portvalue**条目值设置为旧 COM 端口子项下**DosDevices**条目值的值。 对于序列复制的所有其他输入值，它会保留相同的条目值名称。 有关串行复制的入口值的详细信息，请参阅 Microsoft Windows 驱动程序工具包（WDK）中提供的串行示例代码。

**IoReportDetectedDevice**调用将端口标记为根枚举设备。 在后续系统启动时，即插即用管理器会根据其 INF 文件中的信息自动配置设备。

即插即用 manager 为旧 COM 端口创建以下[兼容 id](https://docs.microsoft.com/windows-hardware/drivers/install/compatible-ids) ： DETECTEDInternal\\串行，并检测\\串行。

