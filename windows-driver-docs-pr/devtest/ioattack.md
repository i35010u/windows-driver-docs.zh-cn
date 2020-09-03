---
title: IoAttack
description: 渗透测试 (设备基础) 测试、运行 i/o 攻击、执行模糊测试
ms.assetid: ae0eda5c-534e-44c2-a997-66fe1337ca9f
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08af7b67172fba6b027d30fe316883bec473afce
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384543"
---
# <a name="ioattack"></a>IoAttack

> [!NOTE]
> Windows 10 1703 版后，WDK 中不再提供 IoSpy 和 IoAttack。
>
> 作为这些工具的替代方法，请考虑使用在 HLK 中提供的模糊化测试。 下面是一些需要考虑的事项。
> 
> [DF - 模糊随机 IOCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF - 模糊 sub-open 测试（可靠性）](/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF - 模糊随机 FSCTL 测试（可靠性）](/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF - 模糊杂项 API 测试（可靠性）](/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> 你还可以使用驱动程序验证程序附带的 [内核同步延迟模糊](./kernel-synchronization-delay-fuzzing.md) 处理。
>


[渗透测试 (设备基础) ](penetration-tests--device-fundamentals-.md)测试**运行 i/o 攻击**执行模糊测试。 **运行 I/o 攻击**测试使用以前通过 IoSpy 在测试系统上创建的[IoSpy 数据文件](iospy.md)。

在测试系统上运行 IoAttack 之前，必须执行以下操作：

-   在测试计算机上启用内核模式调试。 这是在配置计算机进行测试时执行的，请参阅 [设置计算机以进行驱动程序部署和测试 (WDK 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)，或 [预配用于驱动程序部署和测试 (WDK 8) ](/previous-versions/hh698272(v=vs.85))的计算机。

-   运行 " **启用驱动程序验证程序测试** "，为要测试的设备启用驱动程序堆栈中所有驱动程序的 [驱动程序验证](driver-verifier.md) 程序选项。 特别是，应该启用 " [特殊池](special-pool.md) " 选项。 在 " **添加或删除驱动程序测试** " 对话框中，" **启用驱动程序验证** 程序" 测试在 "所有测试" \\ 驱动程序验证器下。 请参阅[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)。 有关选择和配置测试和工具参数的信息，请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers)

-   从测试系统中删除 [IoSpy](iospy.md) 。 为此，请运行 **禁用 I/o 监视** 测试。

如果执行了这些步骤中的任何一个，则必须在运行 IoAttack 之前重新启动测试系统。

有关如何运行模糊测试的详细信息，请参阅 [如何通过 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)。

 

