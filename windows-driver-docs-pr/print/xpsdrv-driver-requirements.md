---
title: XPSDrv 驱动程序要求
description: XPSDrv 驱动程序要求
ms.assetid: 382b53eb-a69a-452a-8403-876640a9129e
keywords:
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c3efb47330018a2d1a4c37f27764cd215af6f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390234"
---
# <a name="xpsdrv-driver-requirements"></a>XPSDrv 驱动程序要求


框中， [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，XPSDrv 配置模块必须满足以下要求：

-   XPSDrv 打印机驱动程序必须实现版本 3 打印驱动程序配置模块。

-   配置模块必须支持所有的 PrintTicket 和 PrintCapabilities 功能。 Unidrv 和 Pscript5 打印机驱动程序的 Windows Vista 版本自动提供此支持。 有关如何将此支持添加到的单体式基于 GDI 的版本 3 的打印机驱动程序的详细信息，请参阅[整体式打印驱动程序添加打印票证支持](adding-print-ticket-support-to-monolithic-print-drivers.md)。

配置模块要求的完整列表，请参阅[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。

 

 




