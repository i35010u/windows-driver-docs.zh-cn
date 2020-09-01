---
title: Windows 内核模式配置管理器
description: Windows 内核模式配置管理器
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a29de2af3845f738ee3ed69dd3f17f273dee0c36
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187043"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows 内核模式配置管理器


在 Microsoft Windows、应用程序和操作系统的以前几天中存储的配置值 () 文件中进行初始化。 这提供了一种简单的方法来存储可从一个 Windows 会话保存到下一个 Windows 会话的状态值。 但是，随着 Windows 环境变得更加复杂，需要一个新系统来存储有关操作系统和应用程序的持久信息。 创建 Windows 注册表以存储有关硬件和软件的数据。

Windows 内核模式配置管理器管理注册表。 如果你的驱动程序需要了解注册表中的更改，则可以使用配置管理器的例程通过在特定注册表数据上注册回调来实现此目的。 然后，当注册表中的数据更改时，将触发回调，你可以运行代码来处理驱动程序中的回调信息。

向配置管理器提供直接接口的例程带有字母 "**Cm**" 的前缀;例如， **CmRegisterCallback**。 有关 configuration manager 例程的列表，请参阅 [Configuration Manager 例程](/windows-hardware/drivers/ddi/_kernel/#configuration-manager-routines)。

除了直接调用配置管理器之外，还可以通过其他方式使用驱动程序中的注册表。 有关使用驱动程序中的注册表的详细信息，请参阅 [注册表项对象例程](registry-key-object-routines.md) 和 [驱动程序的注册表项](../install/overview-of-registry-trees-and-keys.md)。

 

