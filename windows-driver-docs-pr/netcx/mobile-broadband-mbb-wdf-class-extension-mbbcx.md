---
title: 移动宽带 (MBB) WDF 类扩展 (MBBCx) 的简介
description: 移动宽带（MBB） WDF 类扩展（MBBCx）的概述。
ms.assetid: FA4D1C2D-270B-40C4-A922-8ABDDE4D8444
keywords:
- Mobile 宽带（MBB） WDF 类扩展，MBBCx，Mobile 宽带 NetAdapterCx
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 47ae8376e181e11a966d3bb5ab25c0dea7794214
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835536"
---
# <a name="introduction-to-the-mobile-broadband-mbb-wdf-class-extension-mbbcx"></a>移动宽带 (MBB) WDF 类扩展 (MBBCx) 的简介

[!include[MBBCx Beta Prerelease](../mbbcx-beta-prerelease.md)]

从 Windows 10 的下一版本开始，Windows 驱动程序工具包（WDK）包含一个适用于 NetAdapterCx 的移动宽带（MBB） WDF 类扩展。 MBB Get-netadapter 客户端驱动程序是最先和最重要的 WDF 客户端驱动程序，那么它们就像其他 NIC 驱动程序一样 NetAdapterCx 客户端驱动程序，最后是 MBB 类扩展（MBBCx）的客户端驱动程序，该驱动程序提供特定于 MBB 媒体的性能. 以下块图说明了 MBBCx 的体系结构：

![MbbCx 体系结构](images/MbbCx.png)

MBB Get-netadapter 客户端驱动程序基于与框架的关系，执行3类任务：

- 为日常设备任务（例如 Pnp 和电源管理）调用[标准 WDF api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/) 。
- 为常见网络设备操作（例如传输或接收网络数据包）调用[NetAdapterCx api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/#netadaptercx) 。
- 为 MBB 特定的控制路径操作（如 MBIM 消息处理）调用[MbbCx api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/#mbbcx) 。

在开始之前，应熟悉以下概念：

- [Windows Driver Foundation （WDF）](../wdf/using-the-framework-to-develop-a-driver.md)
- [Get-netadapter 类扩展（NetAdapterCx）](index.md)

本部分中的主题假定你已了解如何为基本 NIC 编写 NetAdapterCx 客户端驱动程序，因此它们只关注特定于 MBBCx 的代码。

本部分包含以下主题：

- [编写 MBBCx 客户端驱动程序](writing-an-mbbcx-client-driver.md)
