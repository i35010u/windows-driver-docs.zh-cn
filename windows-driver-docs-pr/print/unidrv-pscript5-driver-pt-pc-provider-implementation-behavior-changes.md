---
title: Unidrv/PScript5 驱动程序 PT/PC 提供程序实现行为
description: Unidrv 和 PScript5 驱动程序 PrintTicket 或打印提供程序 (PT/PC) 实现的行为更改
ms.assetid: ff401ae8-b0c5-4f20-88dd-055a14e1d065
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f2ab471bb1cef99cf832a10c1577691aa29bfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554268"
---
# <a name="unidrvpscript5-driver-ptpc-provider-implementation-behavior-changes"></a>Unidrv/PScript5 驱动程序 PT/PC 提供程序实现的行为更改


当运行在 XPSDrv 模式、 Unidrv 或 PScript5 驱动 PrintTicket 或打印提供程序 (PT/PC) 实现还必须禁用任何 Unidrv/PScript5 硬编码功能。 也就是说，PrintCapabilities XML 不应包含任何硬编码 capabiity，并且默认 PrintTicket 或经验证的 PrintTicket 不应包含任何硬编码功能。

 

 


