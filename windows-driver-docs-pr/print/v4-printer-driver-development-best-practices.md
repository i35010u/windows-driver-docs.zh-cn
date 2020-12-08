---
title: V4 打印机驱动程序开发最佳做法
description: 由于 v4 打印机驱动程序是直接从驱动程序存储区调用的，并且它们也应该与低权限应用程序（如 Internet Explorer）进行通信，因此在开发 v4 打印机驱动程序时，请务必遵循建议的最佳实践。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3651dd2207ebd05b3088bd018a1b11fc0defc7d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785885"
---
# <a name="v4-printer-driver-development-best-practices"></a>V4 打印机驱动程序开发最佳做法


由于 v4 打印机驱动程序是直接从驱动程序存储区调用的，并且它们也应该与低权限应用程序（如 Internet Explorer）进行通信，因此在开发 v4 打印机驱动程序时，请务必遵循建议的最佳实践。

本部分介绍以下主题：

[使用驱动程序存储](working-with-the-driver-store.md)

[使用增强的点和打印效果良好](working-well-with-enhanced-point-and-print.md)

[V4 打印机驱动程序安全注意事项](v4-printer-driver-security-considerations.md)

有关打印机驱动程序开发最佳实践的详细信息，请参阅 [开发打印机驱动程序的最佳实践指南](/previous-versions/windows/hardware/design/dn653553(v=vs.85))。

 

