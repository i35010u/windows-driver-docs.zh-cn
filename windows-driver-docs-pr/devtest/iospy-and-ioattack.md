---
title: IoSpy 和 IoAttack
description: IoSpy 和 IoAttack
ms.assetid: 4cc5bf5c-f9e4-43d4-8532-dd7813b6f2a0
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8ee226ee52ab9754fc21be11fa9406dea3ce144
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356521"
---
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


# <a name="iospy-and-ioattack"></a>IoSpy 和 IoAttack


IoSpy 和 IoAttack 是执行 IOCTL 和 WMI 的工具模糊测试对内核模式驱动程序。 通过使用这些工具，可以确保该驱动程序的 IOCTL WMI 代码正确和验证数据缓冲区和缓冲区长度。 通过执行此操作，可以避免缓冲区溢出可能会导致系统不稳定。

*模糊测试*驱动程序提供随机数据，称为*模糊*，从而确定驱动程序中的缺陷。 模糊测试通过 IOCTL 或 WMI 接口并不新鲜。 但是，大多数测试套件是泛型*的黑色框*模糊测试，只能验证驱动程序的 IOCTL 或 WMI 接口，从外部访问或写入测试驱动程序内的特定 IOCTL 和 WMI 路径。

IoSpy 和 IoAttack 使用多个*白色框*模糊测试的方法。 启用设备后的模糊测试，IoSpy 捕获发送到设备的驱动程序的 IOCTL 和 WMI 请求并记录这些请求的数据文件中的属性。 IoAttack 然后从此数据文件，读取特性，并使用这些特性*模糊*，或随机的更改，然后将它们发送到驱动程序的各种方式 IOCTL 或 WMI 请求。 这允许而无需编写特定于 IOCTL 或 WMI 测试的更多的驱动程序缓冲区验证代码中的条目。

运行 Windows Vista 或更高版本的 Windows 操作系统的系统上支持 IoSpy 和 IoAttack。 这些工具包括在为属于 WDK 的一部分[设备基础测试](device-fundamentals-tests.md)，请参阅[渗透测试 （设备基础）](coverage-tests--device-fundamentals-.md)。 可以选择从这些测试**添加或删除驱动程序测试**对话框中的，在 Basic\\设备基础\\渗透\\IoSpy 和攻击的文件夹。

**重要**   IoSpy 和 IoAttack 应在运行之前针对内核模式调试准备的测试系统上。

 

本部分包括以下主题：

[IoSpy](iospy.md)

[IoAttack](ioattack.md)

[如何使用 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)

 

 





