---
title: GetPrintCapabilities
description: IPrintTicketProvider GetPrintCapabilities 例程必须返回有效的 PrintCapabilities 文档。
keywords:
- GetPrintCapabilities
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 084d11a50d98a4936a551c20488c3cd20a6a8aed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796897"
---
# <a name="getprintcapabilities"></a>GetPrintCapabilities


[**IPrintTicketProvider：： GetPrintCapabilities**](/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))例程必须返回有效的 PrintCapabilities 文档。 对于基本实现，文档可能非常简单，但打印驱动程序不支持 PrintCapabilities 文档中未公开的打印票证中的任何功能。 将打印票证支持添加到打印驱动程序时，需要返回到此例程，并将这些功能添加到 PrintCapabilities 文档中。

即使系统通过 DEVMODE 到 PrintTicket 转换来提供的功能，系统也不提供任何默认的 PrintCapabilities 文档。 打印驱动程序必须创建并返回相应的 PrintCapabilities 文档。

 

