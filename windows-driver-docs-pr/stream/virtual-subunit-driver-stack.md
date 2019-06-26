---
title: 虚拟子单元驱动程序堆栈
description: 虚拟子单元驱动程序堆栈
ms.assetid: 5aa1804f-b871-4577-8e8a-ce4ad5150ee0
keywords:
- 虚拟子单元驱动程序堆栈 WDK AV/C
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- 子单元支持 WDK AV/C
- AV/C WDK，驱动程序堆栈
- Avc.sys 功能驱动程序 WDK，驱动程序堆栈
- 兼容 Id WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7ef4094622fb17a79aa145ccf51573ff728c54d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385362"
---
# <a name="virtual-subunit-driver-stack"></a>虚拟子单元驱动程序堆栈


IEEE 1394 驱动程序堆栈可以配置为公开的 IEEE 1394、 IEC 61883 和音频/视频 (AV/C) 控制协议驱动程序通过 IEEE 1394 总线上的其他 AV/C 子单元连接到的系统硬件。 此配置称为虚拟的 IEEE 1394 设备支持。 *Avc.sys*利用这一功能可使计算机成为虚拟 IEEE 1394 设备上的 IEEE 1394 总线其他物理 AV/C 单位。

*Avc.sys*虚拟驱动程序堆栈包含加载来为 IEEE 1394 总线上的虚拟 AV/C 单元表示功能和的计算机的资源的子单元驱动程序。 虚拟子单元堆栈正是*Avc.sys*的计算机中实现通过软件 AV/C 规范。 如果任何计算机的资源将公开为 AV/C 子单元实例化一个虚拟的 AV/C 驱动程序堆栈。

Windows 将加载*Avc.sys*提供虚拟 AV/C 子单元支持基于使用 I/O 控制 (Ioctl) 指定在 INF 文件中或通过应用程序控制的注册表设置。 每个实例*Avc.sys* ，它是加载来支持虚拟子单元注册的新实例的 guid\_虚拟\_AVC\_类设备接口。 有关 GUID 的详细信息\_虚拟\_AVC\_类设备接口，请参阅[使用 Avc.sys](using-avc-sys.md)并[ **IOCTL\_AVC\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ni-avc-ioctl_avc_class)。

注册表是持久的方式保存 AV/C （和更普遍的情况 IEEE 1394） 虚拟设备配置，但虚拟设备配置必须不手动输入到注册表。 相反，配置必须设置使用 INF 文件或通过 Ioctl 的组合。 有关虚拟设备配置的详细信息请参阅[AV/C 设备 Id](av-c-device-identifiers.md)并[虚拟子单元设备 Id](virtual-subunit-device-identifiers.md)。

虚拟的 IEEE 1394 设备提供了以下支持：

-   若要在软件尚不存在的硬件中实现的功能。 此功能允许新硬件来构建原型，可用于测试新的子单元驱动程序开发之前物理硬件。

-   开发自动功能测试套件的对等子单元驱动程序而无需实际的硬件存在。 此功能允许的边界的错误条件的其他方面不是可能的硬件设备可用，一系列测试，它减少了昂贵的硬件测试所针对的需要。

-   若要实现 AV/C 子单元目标功能，例如身份验证和密钥交换 （生成） 和由第三方的计算机上的连接和兼容性管理 (CCM) 协议的扩展的功能。

 

 




