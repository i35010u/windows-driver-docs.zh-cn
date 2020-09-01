---
title: 在注册表中启用消息信号中断
description: 在注册表中启用消息信号中断
ms.assetid: 802ad994-51e7-4aef-a0f0-865dfaf4e6ce
keywords:
- 消息-已发出信号中断 WDK 内核，启用
- 启用邮件终止的 WDK 内核
- Msi WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04160e22ab25b79b639351f271886863484e03c1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191171"
---
# <a name="enabling-message-signaled-interrupts-in-the-registry"></a>在注册表中启用消息信号中断


若要接收 (Msi) 的消息终止中断，驱动程序的 INF 文件必须在安装期间启用注册表中的 Msi。 使用设备硬件密钥的 " **中断管理 \\ MessageSignaledInterruptProperties** " 子项启用 MSI 支持。

**中断管理 \\ MessageSignaledInterruptProperties**的**MSISUPPORTED**条目是一个注册表 \_ DWORD 值，用于确定设备是否支持 msi。 将 **MSISupported** 设置为1可启用 MSI 支持。

你还可以使用注册表指定为其设备分配的最大 Msi 数。 **中断管理 \\ MessageSignaledInterruptProperties**的**MESSAGENUMBERLIMIT**条目是一个 REG \_ DWORD 值，指定要分配的 msi 的最大数目。 对于 PCI 2.2， **MessageNumberLimit** 必须为1、2、4、8或16。 对于 PCI 3.0， **MessageNumberLimit** 可以是任意数量，最多可达2048。

使用驱动程序的 INF 文件中的 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 设置设备硬件密钥下的注册表项。 有关详细信息，请参阅 [**INF DDInstall 部分**](../install/inf-ddinstall-hw-section.md)。

下面的代码示例演示如何在设备的**中断管理 \\ MessageSignaledInterruptProperties**下设置**MSISupported**项。 请注意，必须先创建 **中断管理** 和 **中断管理 \\ MessageSignaledInterruptProperties** 密钥，然后才能设置 **MSISupported** 条目。

```cpp
[mydevice.HW]
AddReg = mydevice_addreg

[mydevice_addreg]
HKR,Interrupt Management,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,MSISupported,0x00010001,1
```

 

