---
title: Windows 内核模式配置管理器
description: Windows 内核模式配置管理器
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 074f89e6b4dd93398e6d64fb3a624d89466fe73c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383189"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows 内核模式配置管理器


在 Microsoft Windows 的早期阶段，应用程序和操作系统存储配置值"INI"（初始化） 文件中。 这提供一种简单的方式来存储状态到下一个可能从一个 Windows 会话中保留的值。 但是，如 Windows 环境变得更复杂，需要存储有关操作系统和应用程序的持久性信息的新系统。 创建 Windows 注册表来存储有关硬件和软件的数据。

Windows 内核模式下配置管理器管理注册表。 如果您的驱动程序需要知道在注册表中的更改，它可以使用 configuration manager 的例程的注册特定的注册表数据的回调。 然后，在注册表中的数据更改时，触发回调，并可以运行代码来处理您的驱动程序中的回调信息。

提供到 configuration manager 的直接接口的例程都带有前缀字母"**Cm**"; 例如， **CmRegisterCallback**。 配置管理器例程的列表，请参阅[配置管理器例程](https://msdn.microsoft.com/library/windows/hardware/ff542038)。

除了直接调用配置管理器，有想要使用的注册表中您的驱动程序的其他方法。 有关使用的注册表中的驱动程序的详细信息，请参阅[使用到的驱动程序注册表](using-the-registry-in-a-driver.md)并[驱动程序的注册表项](https://msdn.microsoft.com/library/windows/hardware/ff549538)。

 

 




