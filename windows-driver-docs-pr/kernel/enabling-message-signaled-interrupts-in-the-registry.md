---
title: 在注册表中启用消息信号中断
description: 在注册表中启用消息信号中断
ms.assetid: 802ad994-51e7-4aef-a0f0-865dfaf4e6ce
keywords:
- 消息信号中断 WDK 内核，启用
- 启用消息信号中断 WDK 内核
- Msi WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b3c804ea0c3224e19461c7455925f278708056f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384942"
---
# <a name="enabling-message-signaled-interrupts-in-the-registry"></a>在注册表中启用消息信号中断


若要接收消息信号中断 (Msi)，驱动程序的 INF 文件必须在安装过程中启用 msi，然后在注册表中。 使用**中断管理\\MessageSignaledInterruptProperties**子项的设备的硬件密钥来启用 MSI 的支持。

**MSISupported**的条目**中断管理\\MessageSignaledInterruptProperties**是 REG\_DWORD 值，该值确定设备是否支持 Msi。 设置**MSISupported**为 1，以启用 MSI 的支持。

此外可以使用注册表来指定要为其设备分配的 Msi 的最大数目。 **MessageNumberLimit**的条目**中断管理\\MessageSignaledInterruptProperties**是 REG\_DWORD 值，该值指定到 Msi 的最大数目分配。 有关 PCI 2.2 **MessageNumberLimit**必须是 1、 2、 4、 8 或 16。 PCI 3.0 **MessageNumberLimit**可以是任意数量最多 2,048。

使用[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)驱动程序的 INF 文件以设置设备的硬件密钥下的注册表项中。 有关详细信息，请参阅[ **INF DDInstall.HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。

下面的代码示例演示如何设置**MSISupported**下的条目**中断管理\\MessageSignaledInterruptProperties**设备。 请注意，您必须首先创建**中断管理**并**中断管理\\MessageSignaledInterruptProperties**密钥才能设置**MSISupported**条目。

```cpp
[mydevice.HW]
AddReg = mydevice_addreg

[mydevice_addreg]
HKR,Interrupt Management,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,,0x00000010
HKR,Interrupt Management\MessageSignaledInterruptProperties,MSISupported,0x00010001,1
```

 

 




