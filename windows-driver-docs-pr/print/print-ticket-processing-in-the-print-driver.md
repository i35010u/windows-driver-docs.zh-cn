---
title: 打印驱动程序中的打印票证处理
description: 打印驱动程序中的打印票证处理
keywords:
- 打印入场券 WDK，打印驱动程序处理
- 打印票证 WDK，XPSDrv
- 打印入场券 WDK，基于 GDI 的打印驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce688855243b33c69e9fa86e73387d4e2001876f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807405"
---
# <a name="print-ticket-processing-in-the-print-driver"></a>打印驱动程序中的打印票证处理


PrintTicket 对象中经过验证的设置用于配置 XPSDrv 打印驱动程序执行的打印处理。 因此，打印驱动程序的组件必须在驱动程序执行任何处理之前读取和解释打印票证中的设置，以便驱动程序可以根据这些设置处理文档。

XPSDrv 打印驱动程序在打印驱动程序的打印处理筛选器中执行此处理。

由于内置于 Windows Vista 打印子系统中的兼容性支持，基于 GDI 的打印驱动程序将继续使用 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构进行设置。 有关此支持的详细信息，请参阅 [打印票证与 Win 32 应用程序的兼容性](print-ticket-compatibility-with-win-32-applications.md)。

有关在打印驱动程序中实现打印票证处理的详细信息，请参阅 [XPSDrv Render 模块中的打印票证支持](print-ticket-support-in-the-xpsdrv-render-module.md)。

 

