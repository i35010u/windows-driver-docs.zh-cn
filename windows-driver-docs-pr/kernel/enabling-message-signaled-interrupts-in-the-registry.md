---
title: 在注册表中启用消息信号中断
description: 在注册表中启用消息信号中断
keywords:
- 消息-已发出信号中断 WDK 内核，启用
- 启用邮件终止的 WDK 内核
- Msi WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1b077f36cccd8068de31cf8c413d89ecf72e39
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790543"
---
# <a name="enabling-message-signaled-interrupts-in-the-registry"></a>在注册表中启用消息信号中断


若要接收 (Msi) 的消息终止中断，驱动程序的 INF 文件必须在安装期间启用注册表中的 Msi。 使用设备硬件密钥的 " **中断管理 \\ MessageSignaledInterruptProperties** " 子项启用 MSI 支持。

**中断管理 \\ MessageSignaledInterruptProperties** 的 **MSISUPPORTED** 条目是一个注册表 \_ DWORD 值，用于确定设备是否支持 msi。 将 **MSISupported** 设置为1可启用 MSI 支持。

你还可以使用注册表指定为其设备分配的最大 Msi 数。 **中断管理 \\ MessageSignaledInterruptProperties** 的 **MESSAGENUMBERLIMIT** 条目是一个 REG \_ DWORD 值，指定要分配的 msi 的最大数目。 对于 PCI 2.2， **MessageNumberLimit** 必须为1、2、4、8或16。 对于 PCI 3.0， **MessageNumberLimit** 可以是任意数量，最多可达2048。

使用驱动程序的 INF 文件中的 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 设置设备硬件密钥下的注册表项。 有关详细信息，请参阅 [**INF DDInstall 部分**](../install/inf-ddinstall-hw-section.md)。

下面的代码示例演示如何在设备的 **中断管理 \\ MessageSignaledInterruptProperties** 下设置 **MSISupported** 项。 请注意，必须先创建 **中断管理** 和 **中断管理 \\ MessageSignaledInterruptProperties** 密钥，然后才能设置 **MSISupported** 条目。

```cpp
[mydevice.HW]
AddReg = mydevice_addreg

[mydevice_addreg]
HKR,Interrupt Management,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,MSISupported,0x00010001,1
```

 

