---
title: 移动宽带 (MBB) WDF 类扩展 (MBBCx) 的简介
description: 移动宽带 (MBB) WDF 类扩展的概述 (MBBCx) 。
keywords:
- Mobile 宽带 (MBB) WDF 类扩展，MBBCx，Mobile 宽带 NetAdapterCx
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: d88e2c029ff4a5090e7417677555636e8510c6b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838856"
---
# <a name="introduction-to-the-mobile-broadband-mbb-wdf-class-extension-mbbcx"></a>移动宽带 (MBB) WDF 类扩展 (MBBCx) 的简介

从 Windows 10 的下一版本开始，Windows 驱动程序工具包 (WDK) 包含一个适用于 NetAdapterCx 的移动宽带 (MBB) WDF 类扩展。 MBB-NetAdapter 客户端驱动程序首先是最先进的 NetAdapterCx 客户端驱动程序，那么它们就像其他 NIC 驱动程序一样是客户端驱动程序，而是 MBB 类扩展的客户端驱动程序 (MBBCx) ，它提供了 MBB 的媒体特定功能。 以下块图说明了 MBBCx 的体系结构：

![MbbCx 体系结构](images/MbbCx.png)

MBB-NetAdapter 的客户端驱动程序将基于其与框架的关系执行3类任务：

- 为日常设备任务（例如 Pnp 和电源管理）调用 [标准 WDF api](/windows-hardware/drivers/ddi/_wdf/) 。
- 为常见网络设备操作（例如传输或接收网络数据包）调用 [NetAdapterCx api](/windows-hardware/drivers/ddi/_netvista/#netadaptercx) 。
- 为 MBB 特定的控制路径操作（如 MBIM 消息处理）调用 [MbbCx api](/windows-hardware/drivers/ddi/_netvista/#mbbcx) 。

在开始之前，应熟悉以下概念：

- [Windows Driver Foundation (WDF) ](../wdf/using-the-framework-to-develop-a-driver.md)
- [Get-netadapter 类扩展 (NetAdapterCx) ](index.md)

本部分中的主题假定你已了解如何为基本 NIC 编写 NetAdapterCx 客户端驱动程序，因此它们只关注特定于 MBBCx 的代码。

本节包含下列主题：

- [编写 MBBCx 客户端驱动程序](writing-an-mbbcx-client-driver.md)
