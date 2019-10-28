---
title: Windows 内核模式配置管理器
description: Windows 内核模式配置管理器
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7dbae31bc252300f1e62abdf27b5f869e4cfd42d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838310"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows 内核模式配置管理器


在 Microsoft Windows 的早期几天，应用程序和操作系统将配置值存储在 "INI" （初始化）文件中。 这提供了一种简单的方法来存储可从一个 Windows 会话保存到下一个 Windows 会话的状态值。 但是，随着 Windows 环境变得更加复杂，需要一个新系统来存储有关操作系统和应用程序的持久信息。 创建 Windows 注册表以存储有关硬件和软件的数据。

Windows 内核模式配置管理器管理注册表。 如果你的驱动程序需要了解注册表中的更改，则可以使用配置管理器的例程通过在特定注册表数据上注册回调来实现此目的。 然后，当注册表中的数据更改时，将触发回调，你可以运行代码来处理驱动程序中的回调信息。

向配置管理器提供直接接口的例程带有字母 "**Cm**" 的前缀;例如， **CmRegisterCallback**。 有关 configuration manager 例程的列表，请参阅[Configuration Manager 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

除了直接调用配置管理器之外，还可以通过其他方式使用驱动程序中的注册表。 有关在驱动程序中使用注册表的详细信息，请参阅使用驱动程序[中的注册表](using-the-registry-in-a-driver.md)和驱动程序的[注册表项](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)。

 

 




