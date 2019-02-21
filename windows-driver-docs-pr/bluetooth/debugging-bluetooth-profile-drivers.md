---
title: 调试蓝牙驱动程序
description: 调试蓝牙驱动程序
ms.assetid: 3c04017e-7f5c-49d4-ad7e-36c7405133a1
keywords:
- 调试配置文件驱动程序 WDK 蓝牙
- 蓝牙 WDK，调试配置文件驱动程序
- 调试驱动程序 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙，调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecaf8b97b1ce29faf84cecef41e4e5d7f339d44e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542949"
---
# <a name="debugging-bluetooth-profile-drivers"></a>调试蓝牙驱动程序


虽然开发蓝牙配置文件驱动程序，你可以使用[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)以帮助其调试。

若要启用你必须验证检查[Bthusb.sys 为启用驱动程序验证程序](https://msdn.microsoft.com/library/windows/hardware/ff551729)。 如果不这样做，将禁用验证检查。

若要利用验证检查完全，请确保使用蓝牙请求块 (BRB) 分配例程，例如， [ **BthAllocateBrb** ](https://msdn.microsoft.com/library/windows/hardware/ff536634)并[ **BthInitializeBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536639)，提供的蓝牙驱动程序堆栈[生成并发送 BRBs](building-and-sending-a-brb.md)。 这些例程包括附加功能，可帮助调试配置文件驱动程序。

可帮助验证检查，以捕获以下类型的错误：

-   尝试重新提交 BRB 之前已完成

-   尝试分配或初始化无效 BRB 键入

-   尝试提交大小无效的 BRB

在调试配置文件驱动程序，可以使用 **！ 分析-v**后 BC 调试器命令\_蓝牙\_VERIFIER\_错误以获取错误的说明。

 

 





