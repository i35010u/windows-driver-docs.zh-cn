---
title: 如何使用 IoSpy 和 IoAttack 执行模糊测试
description: 本主题介绍如何使用 IoSpy 和 IoAttack 工具进行模糊测试
ms.assetid: f800e962-2a0f-4039-a479-395a62428b06
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 646c9b4592b3cc23fde1305a14398d761e46f026
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567293"
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

# <a name="how-to-perform-fuzz-tests-with-iospy-and-ioattack"></a>如何使用 IoSpy 和 IoAttack 执行模糊测试


若要通过使用执行模糊测试[IoSpy](iospy.md)并[IoAttack](ioattack.md)，执行以下操作：

1.  安装[IoSpy](iospy.md):

    若要安装 IoSpy 并启用特定设备上的模糊测试，运行**启用 I/O Spy**测试。 *DQ*参数控制哪些设备安装 IoSpy 筛选器驱动程序。

2.  指定设备上运行 IOCTL 和 WMI 测试：

    测试系统中，重新启动后[IoSpy](iospy.md)已准备好筛选 IOCTL 和 WMI 请求到模糊测试过程中已启用的设备。 现在必须格外 IOCTL 和适当使用任何测试这些设备的驱动程序中的 WMI 代码路径。 这允许 IoSpy 来尽可能基于这些 IOCTL 和 WMI 请求记录尽可能多的详细信息。 IoSpy 将保存在这些详细信息[IoSpy 数据文件](iospy.md)。

3.  卸载 IoSpy:

    您完全执行 IOCTL 和 WMI 代码路径后，必须先卸载 IoSpy，然后才能运行 IoAttack 执行模糊测试。 若要卸载[IoSpy](iospy.md)，请运行**禁用 I/O Spy**测试。

    此命令将删除[IoSpy](iospy.md)从所有已启用模糊测试的设备筛选器驱动程序。 运行该命令后，重新启动的测试系统，才能卸载 IoSpy 筛选器驱动程序从内存。

    **请注意**  时卸载 IoSpy，它不会删除 IoSpy 数据文件。 设置此文件的位置*DFD*参数**启用 I/O Spy**测试。 默认位置是 %systemdrive%\\DriverTest\\IoSpy。 有关详细信息，请参阅[IoSpy 数据文件](iospy.md)。

     

4.  运行[IoAttack](ioattack.md):

    测试系统现在已准备好运行模糊测试运行**运行 I/O 攻击**测试。 有关如何运行 IoAttack 的详细信息，请参阅[IoAttack](ioattack.md)。

    **请注意**  若要验证您的驱动程序 IOCTL 和 WMI 接口的访问权限，应运行[IoAttack](ioattack.md)具有不同权限，如来宾帐户和管理员的帐户帐户。

     

 

 





