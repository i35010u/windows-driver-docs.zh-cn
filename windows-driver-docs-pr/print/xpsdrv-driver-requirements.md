---
title: XPSDrv 驱动程序要求
description: XPSDrv 驱动程序要求
ms.assetid: 382b53eb-a69a-452a-8403-876640a9129e
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv，要求
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 266e48a77fbe1542094a4b50ebd75ea44984f2ae
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793739"
---
# <a name="xpsdrv-driver-requirements"></a>XPSDrv 驱动程序要求

对于内置和[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)，XPSDrv 配置模块必须满足以下要求：

- XPSDrv 打印机驱动程序必须实现版本3打印驱动程序配置模块。

- 配置模块必须支持所有 PrintTicket 和 PrintCapabilities 功能。 Windows Vista 版本的 Unidrv 和 Pscript5 打印机驱动程序自动提供此支持。 若要详细了解如何将此支持添加到基于 GDI 的单一版本3打印机驱动程序，请参阅[将打印票证支持添加到单片打印驱动](adding-print-ticket-support-to-monolithic-print-drivers.md)程序。

有关配置模块要求的完整列表，请参阅[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)。
