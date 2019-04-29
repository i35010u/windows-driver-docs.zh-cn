---
title: 安装旧版 COM 端口
description: 安装旧版 COM 端口
ms.assetid: 9cf2a22c-fb4e-4f15-8410-021d2b4f2ce1
keywords:
- 传统的 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffec5a3b5ba2e6b683702d13dbec7b96afe533e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382755"
---
# <a name="installing-legacy-com-ports"></a>安装旧版 COM 端口





串行函数驱动程序始终配置为旧的串行端口[COM 端口](configuration-of-com-ports.md)。

序列通过读取下的相应 COM 端口子项来检测是否存在旧端口 **...\\Services\\串行\\参数**密钥。 若要安装旧版的 COM 端口，则必须设置一个旧 COM 端口用于此项下设备的子项。 COM 端口子项包含[传统的 COM 端口的注册表设置](registry-settings-for-a-legacy-com-port.md)。

当加载序列它来确定哪些旧端口不以前检测到通过检查**LegacyDiscovered**旧端口条目值。 如果此项值不存在或为零，序列将执行以下任务：

1.  调用[ **IoReportDetectedDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549597)要报告给插管理器的设备。

2.  集**LegacyDiscovered**条目为 0x00000001，指示该端口已报告的端口值。

3.  将一些 COM 端口子项下的条目值复制到物理设备对象的插设备密钥 (*PDO*) 返回由**IoReportDetectedDevice**。

4.  串行集**PortName**插设备密钥的值下的条目值**DosDevices**传统的 COM 端口子项下的项值。 对于所有其他的序列将复制的项值，它将保留相同的项值名称。 有关哪些条目值的详细信息串行复制操作，请参阅提供 Microsoft Windows Driver Kit (WDK) 中的串行示例代码。

**IoReportDetectedDevice**调用标记为根枚举设备的端口。 在后续进行系统启动时，插管理器会自动配置基于其 INF 文件中的信息的设备。

插管理器中创建以下[兼容 Id](https://msdn.microsoft.com/library/windows/hardware/ff539950)为传统的 COM 端口：DETECTEDInternal\\串行和检测到\\串行。

 

 




