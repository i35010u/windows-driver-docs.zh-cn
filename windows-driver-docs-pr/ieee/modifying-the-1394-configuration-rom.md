---
title: 修改 1394 配置 ROM
description: 修改 1394 配置 ROM
keywords:
- IEEE 1394 WDK 总线，修改配置 Rom
- 1394 WDK 总线，修改配置 Rom
- 配置 Rom WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef0e23a0f3e5d2ba221bb8d8dec37e2069686e8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837285"
---
# <a name="modifying-the-1394-configuration-rom"></a>修改 1394 配置 ROM





连接到1394总线的 Microsoft Windows 系统公开了一个配置 ROM，其中描述了该节点支持的功能单元。 有关1394配置 Rom 的详细信息，请参阅 IEEE 1394-1995 和 IEEE-1212-2000 规范。 在 Windows XP 及更高版本的操作系统中，可以通过两种方式动态定义配置 ROM 的内容：

1.  驱动程序可以动态修改配置 ROM，以公开为1394总线上的非1394总线设计的硬件。

    例如，假设有一个常规用途系统，该系统具有连接到系统 IDE 总线的内部 DVD 驱动器。 将1394请求映射到 DVD 驱动器使用的协议的驱动程序可以将1394总线上的 DVD 驱动器公开给其他1394节点。 为此，必须将新的单元目录添加到系统的1394配置 ROM。 然后，连接到1394总线上的其他系统将能够枚举一般用途系统，就像它是 1394 DVD 设备一样。

2.  驱动程序可以使用 (PDOs) 的虚拟物理设备对象来模拟硬件，以简化设备驱动程序的测试。

    设备仿真允许开发人员为尚未收到的设备测试驱动程序。 硬件仿真驱动程序可以在1394总线上公开虚拟1394设备。 然后，开发人员可以在另一个系统上调试新硬件的驱动程序。 有关设备仿真的详细信息，请参阅 [IEEE 1394 硬件仿真驱动程序](./ieee-1394-hardware-emulation-drivers.md)。

## <a name="related-topics"></a>相关主题
[检索 IEEE 1394 节点的配置 ROM 的内容](./retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom.md)
