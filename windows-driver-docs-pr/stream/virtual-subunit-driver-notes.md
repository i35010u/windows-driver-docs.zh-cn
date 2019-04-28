---
title: 虚拟子单元驱动程序说明
description: 虚拟子单元驱动程序说明
ms.assetid: e484f815-73a8-46f1-956e-ee16b1856bd0
keywords:
- Avc.sys 功能驱动程序 WDK，虚拟子单元驱动程序
- 虚拟子单元驱动程序 WDK AV/C
- 外部设备 WDK AV/C
- IOCTL_AVC_CLASS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdc3a6571c1b9e1dd97f32dd6b707ded0ec3bfad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329959"
---
# <a name="virtual-subunit-driver-notes"></a>虚拟子单元驱动程序说明


虚拟子单元驱动程序对控件、 状态和通知 AV/C 请求和响应命令从外部 AV/C 设备通过使用[ **IOCTL\_AVC\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560789)与进行交互*Avc.sys*。

IOCTL\_AVC\_类子函数代码[ **AVC\_函数\_获取\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff554163)和[ **AVC\_函数\_发送\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff554170)是依据虚拟子单元驱动程序与虚拟驱动程序堆栈的其余部分进行交互的主要机制。 虚拟子单元驱动程序提交**AVC\_函数\_获取\_请求**IRP 到*Avc.sys*中其[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)例程 (之后 IRP\_MN\_启动\_设备完成堆栈中的基础驱动程序)。 对于 I/O 完成例程**AVC\_函数\_获取\_请求**IRP 称为每次收到虚拟子单元的请求。 I/O 完成例程必须发送响应 (通过**AVC\_函数\_发送\_响应**与异步 IRP) 内 100 毫秒 （根据 AV/C 协议规则）; 它可能会使用[ **AVC\_命令\_IRB** ](https://msdn.microsoft.com/library/windows/hardware/ff554140)要发送响应的请求中包含的结构。 然后必须重新提交**AVC\_函数\_获取\_请求**IRP 最后从响应的 I/O 完成例程返回之前。

中的虚拟驱动程序堆栈的子单元驱动程序不能直接向外部设备发送命令。 对等方驱动程序堆栈提供此功能。 但是，可以使用虚拟子单元驱动程序[ **AVC\_函数\_查找\_对等方\_执行**](https://msdn.microsoft.com/library/windows/hardware/ff554152)并[ **AVC\_函数\_对等方\_做\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff554168)的 subfunctions [ **IOCTL\_AVC\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560789)发现和引用的对等实例*Avc.sys* ，然后与外部 AV/C 子单元连接进行交互。

为枚举，每个虚拟子单元*Avc.sys*创建相应的设备对象。 因此，添加和删除，虚拟子单元*Avc.sys*触发器 IEEE 1394 总线重置。 此重置允许其他设备上的 IEEE 1394 总线来检测所公开的计算机上的新功能。 虚拟子单元驱动程序已加载根据*Avc.sys*实例的注册表设置并可以添加和删除在运行时通过 IOCTL 代码请求。 请注意， *Avc.sys*无法区分相同类型，因此添加和删除这些子单元连接加载和卸载相应的虚拟子单元驱动程序具有最高的子单元标识符的多个虚拟子单元连接。

虚拟子单元驱动程序可以是胖或瘦。 唯一要求是它会写为 WDM 驱动程序。 胖驱动程序实现大多数，如果不是全部，虚拟设备的功能。 精简的驱动程序提供了虚拟设备功能，它可以是另一个驱动程序或用户模式组件的代理界面。 用户模式和虚拟子单元驱动程序之间的接口是特定于实现的并可通过 IOCTL 代码，专用设备接口实现 (请参阅[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506))或通过[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI)。

即使\_和 MOD\_导致虚拟实例中的 INF 文件中的值为与指定相同*是 61883.sys*加载。 TYP\_和 ID\_时指定的值*Avc.sys*枚举虚拟子单元。

通过实现的虚拟子单元枚举[ **IOCTL\_AVC\_更新\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560798)， [ **IOCTL\_AVC\_删除\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560793)，和[ **IOCTL\_AVC\_总线\_重置**](https://msdn.microsoft.com/library/windows/hardware/ff560783) IOCTL 代码。

必须将正确的 IEEE 1394 Ioctl，发送**IEEE1394\_API\_添加\_虚拟\_设备**并**IEEE1394\_API\_删除\_虚拟\_设备**开始枚举过程。 有关详细信息 (子命令的 IOCTL\_IEEE1394\_API\_请求)。 *61883.inf*文件已包含的设备标识符 (ID) 实现此目的：V1394\\A02D & 10001; 不过，其他标识符，可能会提供自定义的 INF 文件中。

以静态方式枚举虚拟子单元的替代方法可以通过使用 INF 文件。

虚拟设备列表项下的每个值都已打包的子单元地址 （结合使用，如 AV/C 常规规范中所述的子单元类型和最大值标识符）。 与子单元地址关联的名称并不重要，尽管它必须是唯一的该实例。 以编程方式创建，值名称将被赋予顺序编号，以避免冲突。

例如，若要通过 INF 文件创建单个虚拟调谐器子单元，可使用以下**AddReg**指令：

```INF
[Subunit_Device.NT.HW.AddReg]
HKR,%VirtualAvc.DeviceList%,Tuner,0x00000001,0x28 ;0x00000001 = Binary value, 0x28 = Registry key value
```

此指令将添加 REG\_0x28 的二进制值 （子单元类型 0x5 打包到五个最高有效位和最大标识符 0x0 打包到最不明显的三位）。 0x0 此处的最大标识符意味着，将该类型的单个子单元。

**请注意**  :它也是需要定义`%VirtualAvc.DeviceList%`令牌在`[Strings]`子单元的 INF 文件部分。
