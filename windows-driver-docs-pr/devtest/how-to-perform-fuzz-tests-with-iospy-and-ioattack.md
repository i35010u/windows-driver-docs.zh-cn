---
title: 如何使用 IoSpy 和 IoAttack 执行模糊测试
description: 本主题介绍如何使用 IoSpy 和 IoAttack 工具执行模糊测试
ms.assetid: f800e962-2a0f-4039-a479-395a62428b06
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 955370b3932635f2aa8c0e71fe693a1db7927019
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384829"
---
# <a name="how-to-perform-fuzz-tests-with-iospy-and-ioattack"></a>如何使用 IoSpy 和 IoAttack 执行模糊测试

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


若要使用 [IoSpy](iospy.md) 和 [IoAttack](ioattack.md)执行模糊测试，请执行以下操作：

1.  安装 [IoSpy](iospy.md)：

    若要在)  (的特定设备上安装 IoSpy 并启用模糊测试，请运行 " **启用 I/o Spy** 测试"。 *DQ*参数控制安装 IoSpy 筛选器驱动程序的设备。

2.  在指定的设备上运行 IOCTL 和 WMI 测试：

    重新启动测试系统后， [IoSpy](iospy.md) 已准备好筛选 IOCTL，并向已启用模糊测试的设备发出 WMI 请求。 你现在必须通过使用合适的测试，对这些设备的驱动程序中的 IOCTL 和 WMI 代码路径进行演练。 这允许 IoSpy 根据这些 IOCTL 和 WMI 请求记录尽可能多的详细信息。 IoSpy 将这些详细信息保存在 [IoSpy 数据文件](iospy.md)中。

3.  卸载 IoSpy：

    完全执行了 IOCTL 和 WMI 代码路径之后，必须先卸载 IoSpy，然后才能运行 IoAttack 来执行模糊测试。 若要卸载 [IoSpy](iospy.md)，请运行 **禁用 i/o 监视** 测试。

    此命令从为模糊测试启用的所有设备中删除 [IoSpy](iospy.md) 筛选器驱动程序。 运行该命令后，重新启动测试系统以从内存中卸载 IoSpy 筛选器驱动程序。

    **注意**   在卸载 IoSpy 时，它不会删除 IoSpy 数据文件。 此文件的位置由 *DFD* 参数设置为 **Enable i/o Spy** 测试。 默认位置为% SystemDrive% \\ DriverTest \\ IoSpy。 有关详细信息，请参阅 [IoSpy Data File](iospy.md)。

     

4.  运行 [IoAttack](ioattack.md)：

    测试系统现在可以通过运行 " **运行 I/o 攻击** " 测试来运行模糊测试。 有关如何运行 IoAttack 的详细信息，请参阅 [IoAttack](ioattack.md)。

    **注意**   为了验证驱动程序的 IOCTL 和 WMI 接口的访问权限，应使用不同的权限（如来宾帐户和管理员帐户）运行[IoAttack](ioattack.md)帐户。

     

 

