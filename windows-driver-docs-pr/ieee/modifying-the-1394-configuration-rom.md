---
title: 修改 1394 配置 ROM
description: 修改 1394 配置 ROM
ms.assetid: 3dc4fe53-a26b-44c7-96ef-e7bb6181c958
keywords:
- IEEE 1394 WDK 总线，修改配置 Rom
- 1394 WDK 总线，修改配置 Rom
- 配置 Rom WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f59e2be9a3316b94461e3ef0a3291824da14d8f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385756"
---
# <a name="modifying-the-1394-configuration-rom"></a>修改 1394 配置 ROM





Microsoft Windows 系统连接到 1394年总线公开描述功能单元支持的节点配置 ROM。 有关 1394年配置 Rom 的进一步信息，请参阅 IEEE 1394 1995年和 IEEE 1212 2000年规范。 在 Windows XP 和更高版本操作系统中，配置 ROM 的内容可以动态定义两种方式：

1.  驱动程序可以动态修改配置 ROM 公开面向非 1394年总线 1394年总线上的硬件。

    例如，考虑一个具有内置 DVD 驱动器连接到系统的 IDE 总线的常规用途系统。 将 1394年请求映射到 DVD 驱动器使用的协议的驱动程序可能会暴露给 1394年的其他节点的 1394年总线上的 DVD 驱动器。 若要执行此操作，它必须将新的单元目录添加到系统的 1394年配置 ROM。 然后，其他系统上的 1394年总线连接能够枚举常规用途系统，就好像它是 1394 DVD 设备。

2.  驱动程序可以使用虚拟物理设备对象 (PDOs) 来模拟方式，便于您的设备驱动程序测试的硬件。

    设备模拟允许开发人员测试它们未收到的设备的驱动程序。 硬件仿真驱动程序可以公开 1394年总线上的虚拟 1394年设备。 然后，开发人员可以调试在另一个系统在新硬件的驱动程序。 有关设备模拟功能的详细信息，请参阅[IEEE 1394 硬件仿真驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/ieee-1394-hardware-emulation-drivers)。

## <a name="related-topics"></a>相关主题
[检索 IEEE 1394 节点的配置 ROM 的内容](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)  



