---
title: IoSpy 和 IoAttack
description: IoSpy 和 IoAttack
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71bb6e92a3f001481bf634979072ff06ec56a3b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817481"
---
# <a name="iospy-and-ioattack"></a>IoSpy 和 IoAttack

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

IoSpy 和 IoAttack 是在内核模式驱动程序上执行 IOCTL 和 WMI 模糊测试的工具。 通过使用这些工具，可以确保驱动程序的 IOCTL 和 WMI 代码正确验证数据缓冲区和缓冲区长度。 这样做可以避免缓冲区溢出，从而导致系统不稳定。

*模糊测试* 提供了一个包含随机数据的驱动程序（称为 *模糊*），以便确定驱动程序中的缺陷。 对 IOCTL 或 WMI 接口的模糊测试不是新的。 但是，大多数测试套件是一般的 *黑色框* 模糊测试，这些测试仅验证对驱动程序的 IOCTL 或 wmi 接口的外部访问，或写入以测试驱动程序中的特定 IOCTL 和 WMI 路径。

IoSpy 和 IoAttack 使用更多的 *白框* 方法来模糊测试。 为设备启用模糊测试时，IoSpy 将捕获发送到设备驱动程序的 IOCTL 和 WMI 请求，并将这些请求的属性记录在数据文件中。 然后，IoAttack 从该数据文件中读取属性，并在将这些属性发送到驱动程序之前，使用这些属性来 *模糊* 或随机更改 IOCTL 或 WMI 请求。 这样，便可以进一步进入驱动程序的缓冲区验证代码，而无需编写 IOCTL 或特定于 WMI 的测试。

运行 Windows Vista 或更高版本的 Windows 操作系统的系统支持 IoSpy 和 IoAttack。 这些工具作为 [设备基础测试](device-fundamentals-tests.md)的一部分包含在 WDK 中，请参阅 [渗透测试 (设备基础) ](coverage-tests--device-fundamentals-.md)。 可以从 " **添加或删除驱动程序测试** " 对话框中的 "基本 \\ 设备基础 \\ 渗透 \\ IoSpy & 攻击文件夹" 下选择这些测试。

**重要提示**   应该在以前为内核模式调试准备的测试系统上运行 IoSpy 和 IoAttack。

 

本节包括下列主题：

[IoSpy](iospy.md)

[IoAttack](ioattack.md)

[如何通过 IoSpy 和 IoAttack 执行模糊测试](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)

 

