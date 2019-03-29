---
title: GetPrintCapabilities
description: IPrintTicketProvider GetPrintCapabilities 例程必须返回有效的 PrintCapabilities 文档。
ms.assetid: 9c9bd387-5ea2-4758-a967-190a711cd8c3
keywords:
- GetPrintCapabilities
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47bf7c16538026ef383e32db0d1236322291d7d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562855"
---
# <a name="getprintcapabilities"></a>GetPrintCapabilities


[ **IPrintTicketProvider::GetPrintCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff554365)例程必须返回有效的 PrintCapabilities 文档。 对于基本实现，文档可以非常简单但打印驱动程序不能在不公开 PrintCapabilities 文档中的打印票证支持任何功能。 打印票证支持添加到您的打印驱动程序时，将需要返回到此例程，并将这些功能添加到 PrintCapabilities 文档。

即使对于 DEVMODE PrintTicket 转换通过系统提供的功能，系统不提供任何默认 PrintCapabilities 文档。 打印驱动程序必须创建并返回相应的 PrintCapabilities 文档。

 

 




