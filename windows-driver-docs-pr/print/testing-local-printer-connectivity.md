---
title: 测试本地打印机连接
description: 测试本地打印机连接
ms.assetid: 08a16c04-fc64-4e19-b7f2-7a078bc151a2
keywords:
- 测试驱动程序 WDK 打印机
- 打印机驱动程序 WDK，测试
- 本地打印机测试 WDK
- 连接 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9ed70d8414d1a37c5486595d2c9139f0e71c50
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213083"
---
# <a name="testing-local-printer-connectivity"></a>测试本地打印机连接


本部分提供有关如何测试本地连接的打印机连接的一般准则。 你可以将这些原则应用到连接打印设备的任何总线或端口，但由于你的总线或端口的固有性质，某些原则可能不适用。

**注意**   以下信息介绍了如何在 Microsoft Windows XP 上进行测试。 其他操作系统版本（如 "控制面板应用程序" 和 "菜单选项"）的功能可能略有不同。

 

### <a name="setting-up-device-testing"></a>设置设备测试

在继续对你的设备进行任何测试之前，请确保按如下所示设置调试会话，以捕获可能遇到的任何问题。 有关如何正确设置测试环境的详细说明，请参阅 [调试打印机驱动程序和后台处理程序组件](debugging-printer-drivers-and-spooler-components.md) 。

1.  设置应用程序验证工具，并启用默认设置，以监视 Spoolsv.exe。 建议在各种硬件（包括32和64位计算机）上进行测试。

2.  使用驱动程序验证程序工具监视正在使用的任何内核模式驱动程序。 对于打印机驱动程序，请确保包含 Win32k.sys。 请参阅 [驱动程序验证程序](../devtest/driver-verifier.md) ，了解有关设置测试环境以使用该工具的信息。

3.  对于电源管理测试，在附加设备之前，请确保你的测试环境支持所有可能的系统电源状态，并且设备可以成功进入并唤醒所有状态。

以下部分介绍了测试连接端口的设备时要解决的常见测试方案。

-   [设备安装](device-installation.md)

-   [设备功能](testing-device-functionality.md)

-   [设备错误状态](device-error-states.md)

-   [电源管理](power-management.md)

-   [压力测试](stress-testing.md)

 

