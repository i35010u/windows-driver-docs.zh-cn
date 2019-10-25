---
title: 调试蓝牙配置文件驱动程序
description: 调试蓝牙配置文件驱动程序
ms.assetid: 3c04017e-7f5c-49d4-ad7e-36c7405133a1
keywords:
- 调试配置文件驱动程序 WDK 蓝牙
- 蓝牙 WDK，调试配置文件驱动程序
- 调试驱动程序 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙，调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274fd22c31a334ae9c4b19a335574231939146c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833854"
---
# <a name="debugging-bluetooth-profile-drivers"></a>调试蓝牙配置文件驱动程序


开发蓝牙配置文件驱动程序时，可以使用[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器来帮助进行调试。

若要启用验证检查，必须[为 Bthusb 启用驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-drivers-to-be-verified)。 如果未执行此操作，则将禁用验证检查。

若要完全利用验证检查，请确保使用蓝牙请求块（BRB）分配例程（例如[**BthAllocateBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)和[**BthInitializeBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)），这些例程由蓝牙驱动程序堆栈提供，用于[生成和发送 BRBs](building-and-sending-a-brb.md). 这些例程包含有助于调试配置文件驱动程序的附加功能。

验证检查有助于捕获以下类型的错误：

-   尝试在 BRB 完成之前重新提交

-   尝试分配或初始化无效的 BRB 类型

-   尝试提交大小无效的 BRB

调试配置文件驱动程序时，可以在 BC\_BLUETOOTH\_VERIFIER\_错误后使用 **！分析-v**调试器命令获取错误说明。

 

 





