---
title: 虚拟子单元驱动程序堆栈
description: 虚拟子单元驱动程序堆栈
keywords:
- 虚拟子单位驱动程序堆栈 WDK AV/C
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- 子次级支持 WDK AV/C
- AV/C WDK，驱动程序堆栈
- Avc.sys 函数驱动程序 WDK，驱动程序堆栈
- 兼容 Id WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06ef05a57ec2ea4311206b2d0cb5531e98e0ab43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791089"
---
# <a name="virtual-subunit-driver-stack"></a>虚拟子单元驱动程序堆栈


可以通过 ieee 1394、IEC 61883 和音频/视频控制 (AV/C) 协议驱动程序，将 IEEE 1394 驱动程序堆栈配置为向 IEEE 1394 总线上的其他 AV/C 子单元连接公开系统硬件。 此配置称为虚拟 IEEE 1394 设备支持。 *Avc.sys* 使用此功能使计算机成为 ieee 1394 总线上的其他物理 AV/C 单元的虚拟 IEEE 1394 设备。

*Avc.sys* 的虚拟驱动程序堆栈包含用于将计算机的功能和资源表示为 IEEE 1394 总线上的虚拟 AV/C 单元的子单元驱动程序。 虚拟子单位堆栈是 *Avc.sys* 通过计算机中的软件实现 AV/C 规范的位置。 如果计算机的任何资源将作为 AV/C 子单位公开，则会实例化虚拟 AV/C 驱动程序堆栈。

Windows 将加载 *Avc.sys* 以根据 INF 文件中指定的注册表设置或通过使用 i/o 控件 (IOCTLs) ，提供虚拟 AV/C 子单元支持。 加载以支持虚拟子单位的 *Avc.sys* 的每个实例都注册 GUID \_ virtual \_ AVC \_ 类设备接口的新实例。 有关 GUID \_ VIRTUAL \_ AVC \_ 类设备接口的详细信息，请参阅 [使用 Avc.sys](using-avc-sys.md) 和 [**IOCTL \_ AVC \_ 类**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)。

注册表是保存 AV/C (和更常见的 IEEE 1394) 虚拟设备配置的持久方法，但不能在注册表中手动输入虚拟设备配置。 相反，必须使用 INF 文件或 IOCTLs 的组合来设置配置。 有关虚拟设备配置的详细信息，请参阅 [AV/C 设备 id](av-c-device-identifiers.md) 和虚拟子单位 [设备 id](virtual-subunit-device-identifiers.md)。

虚拟 IEEE 1394 设备提供以下支持：

-   在尚不存在的软件硬件中实现的能力。 此功能允许在物理硬件可测试之前开发原型和新的子单位驱动程序。

-   能够为对等子的驱动程序开发自动测试套件，无需实际硬件。 此功能允许测试边界错误条件，这些错误条件不可能在可用的硬件设备范围内实现，并且可减少对昂贵硬件的测试需求。

-   能够实现对 AV/C 子单位目标功能的扩展，例如身份验证和密钥交换 (请) 以及计算机上第三方 (CCM) 协议的连接和兼容性管理。

 

