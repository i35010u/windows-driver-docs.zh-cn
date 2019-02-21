---
title: 对等子单元驱动程序堆栈
description: 对等子单元驱动程序堆栈
ms.assetid: 6ef4b6ae-3802-4ba9-acfa-4b3edba11ba3
keywords:
- 对等子单元驱动程序堆栈 WDK AV/C
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- 子单元支持 WDK AV/C
- AV/C WDK，驱动程序堆栈
- 单元的命令 WDK AV/C
- 内置扩展机制 WDK AV/C
- 命令扩展机制 WDK AV/C
- 命令目标将 WDK AV/C
- Avc.sys 功能驱动程序 WDK，驱动程序堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1963f859c1ba74a57ffcbce41a0c80a2aa0207f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543624"
---
# <a name="peer-subunit-driver-stack"></a>对等子单元驱动程序堆栈


对等方驱动程序堆栈包含加载来表示，处于活动状态的 IEEE 1394 总线上并可以通过计算机控制的 AV/C 子单元连接的驱动程序。 必须启动通过 AV/C 对等方驱动程序堆栈的外部设备控制。 Windows 将加载的实例*Avc.sys*每个外部 AV/C 设备上的 IEEE 1394 总线只要设备连接到系统 （或在系统启动时存在）。 每个实例*Avc.sys* ，它是加载来支持对等子单元驱动程序注册的新实例的 guid\_AVC\_类设备接口。 有关 GUID 的详细信息\_AVC\_类设备接口，请参阅[使用 Avc.sys](using-avc-sys.md)并[ **IOCTL\_AVC\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560789).

对等子单元驱动程序访问和控制其子单元连接通过 IOCTL\_AVC\_导出的类接口*Avc.sys*。 *Avc.sys*处理 AV/C 命令和响应协议，包括具有 IEC 61883 函数控制协议 (FCP) 的所有交互。 但是，请注意，对等子单元驱动程序不是无法与通信并直接访问某些*是 61883.sys*功能在必要时。 子单元驱动程序可能需要直接与其*是 61883.sys*子单元驱动程序时表示使用 Microsoft 不支持的流格式 AV/C 子单元。 子单元驱动程序可以使用**IOCTL\_61883\_类**接口来直接与通信*是 61883.sys*在必要时。 Microsoft 提供较低的筛选器驱动程序， *Avcstrm.sys*，这可以帮助进行流式处理 DV 和 MPEG2 格式。 有关详细信息*Avcstrm.sys*，请参阅[AV/C 流式处理概述](av-c-streaming-overview.md)。

对等子单元驱动程序可以注册的通知并接收来自外部 AV/C 设备 AV/C 命令。 若要注册，对等子单元驱动程序将发出[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766) 的I/O请求数据包(IRP)**IoControlCode** IOCTL 成员\_AVC\_类 I/O 控制代码和子函数设置为 AVC\_函数\_获取\_请求。 此功能使子单元驱动程序，以便接收来自其子单元 AV/C 请求的对等支持，并且对于规范，例如连接和兼容性管理 (CCM) 协议和数字传输内容保护 (DTCP)... 有关 CCM 的详细信息，请参阅[IEEE 1394 贸易协会](https://go.microsoft.com/fwlink/p/?LinkId=518448)网站。 有关 DTCP 详细信息，请参阅[数字传输许可管理员](https://go.microsoft.com/fwlink/p/?linkid=8731)网站。

请注意此功能旨在支持虚拟 AV/C 子单元驱动程序 （其中子单元驱动程序位于虚拟 AV/C 设备堆栈中） 向计算机发送 AV/C 命令而不允许在外部的设备发送到的 AV/C 命令上的 AV/C 子单元连接计算机系统。

### <a href="" id="peer-stack-as-av-c-command-target"></a>**对等方堆栈上为 AV/C 命令目标**

对等子单元驱动程序堆栈可以包含其他 WDM 筛选器驱动程序提供特定于供应商或特定于设备的目标 AV/C 功能。 通过此对等子单元驱动程序堆栈的扩展机制，第三方供应商可以独立地实现许多增值功能，如 5c 复制保护，以及由 Microsoft 提供的 AV/C 实现的扩展。

子单元驱动程序可以执行此功能，但对于具有多个子单元连接的设备，WDM 筛选器驱动程序是首选的方法。 如果上部驱动程序 （子单元或筛选器驱动程序） 注册以接收传入请求通过，计算机仅公开为 AV/C 目标[ **AVC\_函数\_获取\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff554163). 有关 AV/C 单元命令的详细信息，请参阅[ **AVC\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)。

驱动程序加载基于设备标识符 (Id);因此，单元功能可以有选择地加载特定于设备的或特定于供应商的基础上。 虚拟子单元驱动程序堆栈支持这种机制以一般方式 （不在特定于设备的一种方法）。

请注意，如果对等子单元驱动程序堆栈实现特定于设备的单位扩展、 未经处理的单元的任何命令，以及所有传入的子单元命令，就可以转给[虚拟子单元驱动程序堆栈](virtual-subunit-driver-stack.md)。

### <a name="unit-command-extension-mechanism"></a>**单元命令扩展机制**

在对等子单元驱动程序堆栈的上下文中，目标功能仅限于 AV/C 单元命令的支持。 如果子单元驱动程序 （适用于虚拟子单元或对等子单元） 注册以接收 AV/C 请求，则*Avc.sys*支持仅子单元\_信息 (0x31) 和单元\_直接的信息 (0x30) 操作码。 有关操作码的详细信息，请参阅*AV/C 数字接口命令设置常规规范、 Rev 3.0*。 若要支持其他单元命令，例如 CCM 协议或 DTCP，针对*Avc.sys*提供插件的扩展机制。 任意数量的子单元或 WDM 筛选器驱动程序可以注册它们支持通过的单元操作码**AlternateOpcodes**的成员[ **AVC\_命令\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554140)结构，它通过已提交[ **AVC\_函数\_获取\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff554163)函数。 **AlternateOpcodes**是一个计数的字节数组; 元素 0 是备用操作代码中的剩余字节数。 **AlternateOpcodes**时发送响应，因此不需要的备用操作码处于隐藏状态处理单元请求时，将忽略。

若要使用的内置扩展机制，指定单元地址为中的 0xff **SubunitAddress**成员的 AVC\_命令\_IRB 结构。 **SubunitAddress**处于单独的成员的单元命令 （单元解决提供的子单元驱动程序仍存在）。 虚拟子单元驱动程序都可以使用密钥的中断**SubunitAddress**成员。

 

 




