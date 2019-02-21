---
title: 移动宽带 (MBB) WDF 类扩展 (MBBCx)
description: 移动宽带 (MBB) WDF 类扩展 (MBBCx) 的概述。
ms.assetid: FA4D1C2D-270B-40C4-A922-8ABDDE4D8444
keywords:
- 移动宽带 (MBB) WDF 类扩展，MBBCx，移动宽带 NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 851489e28a5a2928260c6d73958583c71be2cfde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544625"
---
# <a name="mobile-broadband-mbb-wdf-class-extension-mbbcx"></a>移动宽带 (MBB) WDF 类扩展 (MBBCx)

[!include[MBBCx Beta Prerelease](../mbbcx-beta-prerelease.md)]

从 Windows 10 的下一个版本，Windows Driver Kit (WDK) 包括适用于 NetAdapterCx 移动宽带 (MBB) WDF 类扩展。 MBB NetAdapter 客户端驱动程序都是最重要的是齐备的 WDF 客户端驱动程序，则它们 NetAdapterCx 客户端驱动程序就像其他 NIC 驱动程序，并且它们提供特定于 MBB 媒体的 MBB 类扩展 (MBBCx) 的客户端驱动程序的最后功能。 以下块图说明 MBBCx 体系结构：

![MbbCx 体系结构](images/MbbCx.png)

MBB NetAdapter 客户端驱动程序执行任务基于 framework 其关系的 3 个的类别：

- 调用[标准 WDF Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)常见设备的任务，如 Pnp 和电源管理。
- 调用[NetAdapterCx Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/#netadaptercx)针对一些常见的网络设备操作，如传输或接收网络数据包。
- 调用[MbbCx Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/#mbbcx)对于特定于 MBB 的控制路径操作，例如 MBIM 消息处理。

在开始之前，应熟悉这些概念：

- [Windows Driver Foundation (WDF)](../wdf/using-the-framework-to-develop-a-driver.md)
- [NetAdapter 类扩展 (NetAdapterCx)](index.md)

在本部分中的主题假定您已了解如何为基本的 NIC，编写 NetAdapterCx 客户端驱动程序，以便他们仅专注 MBBCx 特有的代码。

本部分包含以下主题：

- [编写 MBBCx 客户端驱动程序](writing-an-mbbcx-client-driver.md)
