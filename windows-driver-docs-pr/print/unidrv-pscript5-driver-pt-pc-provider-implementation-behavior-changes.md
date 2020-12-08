---
title: Unidrv/PScript5 驱动程序 PT/PC 提供程序实现行为
description: Unidrv 和 PScript5 驱动程序 PrintTicket 或打印提供程序 (PT/PC) 实现行为更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34979dd8e7c5b97e29205cff6ee624fa608c8d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833285"
---
# <a name="unidrvpscript5-driver-ptpc-provider-implementation-behavior-changes"></a>Unidrv/PScript5 驱动程序 PT/PC 提供程序实现行为更改


在 XPSDrv 模式下运行时，Unidrv 或 PScript5 驱动程序的 PrintTicket 或打印提供程序 (PT/PC) 实现也必须禁用任何 Unidrv/PScript5 硬编码功能。 也就是说，PrintCapabilities XML 不应包含任何硬编码的 capabiity，且默认的 PrintTicket 或已验证的 PrintTicket 不应包含任何硬编码的特征。

 

 


