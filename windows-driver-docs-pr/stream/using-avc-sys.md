---
title: Using Avc.sys
description: Using Avc.sys
ms.assetid: 3b4ec139-ff01-40bd-8e29-92f554180585
keywords:
- Avc.sys 功能驱动程序 WDK，有关 Avc.sys 函数驱动程序
- AV/C WDK，Avc.sys 使用情况
- 子单元支持 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cc329213f0ce766e2feb1ea6d394ee1debe16a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543933"
---
# <a name="using-avcsys"></a>Using Avc.sys





在 Windows 后加载和初始化*Avc.sys*， *Avc.sys*使用标准 AV/C 单元和子单元命令来发现 AV/C 的所有设备上活动的子单元连接到 （包括任何 IEEE 1394 总线虚拟子单元连接计算机是虚拟的 AV/C 单元时）。 *Avc.sys*然后生成的所有活动的子单元连接的设备标识符 (Id)。 下一步， *Avc.sys*使用标准和插即用 (PnP) 的机制来加载每个次级单位的相应子单元驱动程序。 要加载的子单元驱动程序基于安装子单元驱动程序和子单元的设备标识符的 INF 文件，如生成的所选*Avc.sys*中所述[AV/C 设备 Id](av-c-device-identifiers.md)。 从 AV/C 设备，与子单元的结合使用的单位信息生成的设备标识符***SubunitType***并***SubunitID***字段。 支持子单元的驱动程序可以是特定于供应商，也可以是泛型类型的子单元。 例如，大多数 DV 摄像机的子单元驱动程序是 Microsoft 提供*Msdv.sys*。

子单元驱动程序与通信*Avc.sys*通过采用基于 WDM 体系结构的所有驱动程序的标准基于 IRP 的机制。 子单元驱动程序通过分配并将驱动程序堆栈的下层的 Irp 发送到 AV/C 协议驱动程序，其 AV/C 子单元与通信*Avc.sys*。 若要发出 I/O 请求，包括标头文件*Avc.h*，这提供与 Microsoft Windows Driver Kit (WDK)。

子单元驱动程序分配并初始化由处理 Irp *Avc.sys*。 子单元驱动程序设置 IRP **Parameters.DeviceIoControl.IoControlCode** IOCTL 与所需的 AV/C 操作相对应的成员。

*Avc.sys*注册两个之一[设备接口](https://msdn.microsoft.com/library/windows/hardware/ff543137)根据已加载到的子单元驱动程序堆栈支持 (对等或虚拟)。 这些接口定义的功能， *Avc.sys*导出子单元驱动程序、 其他驱动程序和应用程序使用。 *Avc.sys*然后接口的状态更改为启用或禁用即插即用驱动程序的状态根据。

*Avc.sys*注册一个新实例的 GUID\_AVC\_类如果它已加载为外部 AV/C 子单元 （对等方堆栈） 提供支持。 此接口仅支持以下 I/O 控制 (IOCTL) 代码：

-   [**IOCTL\_AVC\_CLASS**](https://msdn.microsoft.com/library/windows/hardware/ff560789)

IOCTL\_AVC\_类又支持多个函数代码。 子驱动程序的实例*Avc.sys*以支持对等子单元连接保证能够访问其父设备对象通过此接口。

GUID\_AVC\_类接口支持所有 IOCTL\_AVC\_类函数代码，尽管一些具有限制对它们的使用，每个函数的参考页中所述。

*Avc.sys*注册一个新实例的 GUID\_虚拟\_AVC\_类，如果已加载，以便为虚拟 AV/C 子单元连接 （虚拟堆栈） 提供支持。 此接口支持四个 I/O 控制 (IOCTL) 代码：

-   [**IOCTL\_AVC\_CLASS**](https://msdn.microsoft.com/library/windows/hardware/ff560789)

-   [**IOCTL\_AVC\_更新\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560798)

-   [**IOCTL\_AVC\_删除\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560793)

-   [**IOCTL\_AVC\_BUS\_RESET**](https://msdn.microsoft.com/library/windows/hardware/ff560783)

GUID\_虚拟\_AVC\_类接口不支持每个 IOCTL\_AVC\_类函数代码。 每个单个函数代码的参考页用于指定是否支持它的 GUID\_虚拟\_AVC\_的类实例*Avc.sys*。

IOCTL\_AVC\_Irp 类仅支持在内核模式下 （通常用于驱动程序的通信） 通过[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)。 因此，应用程序不能直接访问 IOCTL 所提供的函数\_AVC\_类 IOCTL 代码。

内核模式和通过用户模式中支持的最后三个 IOCTL 代码[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)。 这意味着，应用程序可以发送这些 Ioctl 直接*Avc.sys*。

IOCTL\_AVC\_类 IOCTL 代码必须始终附带由 I/O 请求块 (IRB) 进一步描述要执行的 AV/C 操作。 IRB 标头包含一个函数编号，用于确定 IRB 其余部分的结构。 IRB 结构和大小而异的函数。 *Avc.sys*使用两个自定义 IRBs:

-   [**AVC\_命令\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554140)

-   [**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)

选择 IRB 子单元驱动程序必须使用取决于所需的函数。 详细了解 IOCTL\_AVC\_类支持的函数代码*Avc.sys，* 请参阅[AV/C 协议驱动程序函数代码](https://msdn.microsoft.com/library/windows/hardware/ff556389)。

子单元驱动程序使用的主要 AV/C 功能是[ **AVC\_函数\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff554150)，它使用 AVC\_命令\_IRB 结构。 **AVC\_函数\_命令**发送 AV/C 请求并接收相应的 AV/C 响应。 用于构建 AV/C 命令的详细信息将由*Avc.sys*，但子单元驱动程序必须提供 AV/C 操作码和操作数的每个命令。

 

 




