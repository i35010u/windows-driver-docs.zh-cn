---
title: 测试本地打印机连接
description: 测试本地打印机连接
ms.assetid: 08a16c04-fc64-4e19-b7f2-7a078bc151a2
keywords:
- 测试驱动程序 WDK 打印机
- 打印机驱动程序 WDK，测试
- 测试 WDK 的本地打印机
- 连接 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b3869382216cc8c764a204ac4bc2266eeae9a2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388055"
---
# <a name="testing-local-printer-connectivity"></a>测试本地打印机连接


本部分提供关于如何测试本地连接的打印机的连接性的常规指南。 尽管由于总线或端口的固有性质可能不适用于一些原则，可以对任何总线或打印设备连接到端口应用这些原则。

**请注意**  下列信息描述了在 Microsoft Windows XP 上进行测试。 其他操作系统版本，例如控制面板应用程序和菜单选项的功能可能略有不同。

 

### <a name="setting-up-device-testing"></a>设置设备测试

在继续之前设备的任何测试，请确保设置在调试会话，如下所示来捕获可能会遇到任何问题。 请参阅[调试打印机驱动程序和后台处理程序组件](debugging-printer-drivers-and-spooler-components.md)如何正确设置你的测试环境。

1.  使用默认设置启用监视 Spoolsv.exe 设置应用程序验证器。 在各种硬件上测试，包括 32 位和 64 位计算机，建议。

2.  使用驱动程序验证程序工具来监视正在使用的任何内核模式驱动程序。 打印机驱动程序，请务必包括 Win32k.sys。 请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)有关设置你的测试环境以使用该工具的信息。

3.  有关电源管理测试，附加设备之前，请确保你的测试环境，支持所有可能的系统电源状态和设备可以输入并从所有状态成功唤醒。

测试端口连接设备时，以下部分将介绍解决常见的测试方案。

-   [设备安装](device-installation.md)

-   [设备功能](testing-device-functionality.md)

-   [设备的错误状态](device-error-states.md)

-   [电源管理](power-management.md)

-   [压力测试](stress-testing.md)

 

 




