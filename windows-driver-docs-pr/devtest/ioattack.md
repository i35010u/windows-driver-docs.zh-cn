---
title: IoAttack
description: 渗透测试 （设备基础） 测试，运行 I/O 攻击中，执行模糊测试
ms.assetid: ae0eda5c-534e-44c2-a997-66fe1337ca9f
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3c4f47fa009a8dccc7a388ce9dedaeb6b96a8925
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373708"
---
# <a name="ioattack"></a>IoAttack

> [!NOTE]
> IoSpy 和 IoAttack 不再在 WDK 中可用后 Windows 10 版本 1703年。
>
> 作为这些工具的替代方法，请考虑使用 HLK 中可用的模糊测试。 下面是一些需要考虑。
> 
> [DF - 模糊随机 IOCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF - 模糊 sub-open 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF - 模糊零长度缓冲区 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF - 模糊随机 FSCTL 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF - 模糊杂项 API 测试（可靠性）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> 此外可以使用[内核同步延迟模糊](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)随驱动程序验证程序。
>


[（设备基础） 的渗透测试](penetration-tests--device-fundamentals-.md)测试**运行 I/O 攻击**执行模糊测试。 **运行 I/O 攻击**测试将使用[IoSpy 数据文件](iospy.md)以前创建 IoSpy 通过的测试系统上。

在运行之前 IoAttack 测试系统上，必须执行以下操作：

-   启用内核模式调试在测试计算机上。 这是配置用于测试的计算机时，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)，或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))。

-   运行**启用驱动程序验证工具测试**以启用[Driver Verifier](driver-verifier.md)要测试的设备上所有驱动程序堆栈中的驱动程序选项。 具体而言，应启用[特殊池](special-pool.md)选项。 在中**添加或删除驱动程序测试**对话框中，**启用驱动程序验证程序测试**下的所有测试\\驱动程序验证程序。 请参阅[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关选择和配置测试和工具参数的信息，请参阅[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)

-   删除[IoSpy](iospy.md)从测试系统。 若要执行此操作，请运行**禁用 I/O Spy**测试。

如果执行这些步骤，必须重新启动的测试系统，然后再运行 IoAttack。

有关如何运行模糊测试的详细信息，请参阅[如何使用 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)。

 

 





