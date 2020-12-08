---
title: 调试蓝牙配置文件驱动程序
description: 调试蓝牙配置文件驱动程序
keywords:
- 调试配置文件驱动程序 WDK 蓝牙
- 蓝牙 WDK，调试配置文件驱动程序
- 调试驱动程序 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙，调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff24e28fac3416f7530b611dc456fe58d748cbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798539"
---
# <a name="debugging-bluetooth-profile-drivers"></a>调试蓝牙配置文件驱动程序


开发蓝牙配置文件驱动程序时，可以使用 [驱动程序验证](../devtest/driver-verifier.md) 器来帮助进行调试。

若要启用验证检查，必须 [为 Bthusb.sys启用驱动程序验证程序 ](../devtest/selecting-drivers-to-be-verified.md)。 如果未执行此操作，则将禁用验证检查。

若要充分利用验证检查，请确保使用蓝牙请求块 (BRB) 分配例程（例如 [**BthAllocateBrb**](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb) 和 [**BthInitializeBrb**](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)），这些例程由蓝牙驱动程序堆栈提供，用于 [生成和发送 BRBs](building-and-sending-a-brb.md)。 这些例程包含有助于调试配置文件驱动程序的附加功能。

验证检查有助于捕获以下类型的错误：

-   尝试在 BRB 完成之前重新提交

-   尝试分配或初始化无效的 BRB 类型

-   尝试提交大小无效的 BRB

调试配置文件驱动程序时，可以在 BC 蓝牙验证程序错误后使用 **！分析-v** 调试器命令 \_ \_ \_ 获取错误说明。

 

