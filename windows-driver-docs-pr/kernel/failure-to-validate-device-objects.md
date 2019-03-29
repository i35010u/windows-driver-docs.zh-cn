---
title: 无法验证设备对象
description: 无法验证设备对象
ms.assetid: aa4abc20-0b87-44d7-8987-a5b2be397bb1
keywords:
- 可靠性 WDK 内核，设备对象验证
- 设备对象 WDK 内核，验证失败
- 验证故障 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 531fc5bbc64c16186b528a30cda00c01fc22530a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575692"
---
# <a name="failure-to-validate-device-objects"></a>无法验证设备对象





许多驱动程序创建多个类型的设备对象通过调用[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)。 某些驱动程序创建的控件中的设备对象及其**DriverEntry**例程，从而允许应用程序进行通信的驱动程序，甚至在驱动程序创建 FDO 之前。 例如，文件系统驱动程序创建设备对象来处理文件系统通知时它们将自身注册为文件系统**IoRegisterFileSystem**。

驱动程序应已准备好[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)它会创建任何设备对象的请求。 完成后成功状态的请求，该驱动程序应该会收到任何用户可访问的 I/O 请求上创建的文件对象。 因此，创建多个设备对象的任何驱动程序必须检查每个 I/O 请求指定的设备对象。

例如，假设一个驱动程序创建整个控件中的设备对象[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)，然后创建另一组中的设备对象及其[ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。 假设*AddDevice*例程初始化较低级驱动程序的信息的设备扩展但控制设备对象不包含此信息。 在这种情况下，所有的调度例程必须仔细检查他们收到的每个设备对象。 否则，尝试使用设备扩展信息时，可能会崩溃，驱动程序。

 

 




