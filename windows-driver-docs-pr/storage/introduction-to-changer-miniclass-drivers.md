---
title: 关于转换器 Miniclass 驱动程序
description: 关于转换器 Miniclass 驱动程序
ms.assetid: ce0f78a3-69ae-4ca7-b2e1-f4892e35a230
keywords:
- 转换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK、miniclass 驱动程序
- miniclass 驱动程序 WDK 转换器
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 290eef3135d095147fc5e2d27e3f8331a186eea6
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606561"
---
# <a name="about-changer-miniclass-drivers"></a>关于转换器 Miniclass 驱动程序

为了支持新的转换器，驱动程序编写器实现了一个链接到系统提供的变换器类驱动程序的转换器 miniclass 驱动程序。 必须仅编写一个新的转换器 miniclass 驱动程序，以支持系统尚未提供驱动程序的转换器。

在开始实现新的 miniclass 驱动程序之前，应确保：

- 设备是真正的更换器，而不是串行存取堆栈器。 使用更换器，可以按随机顺序（而不是固定顺序）在其驱动器中装载媒体，就像在原纸器中一样。

- 设备的驱动器不是写入一次光驱，如 WORM、CD-R 或 DVD-R。

- 设备的驱动器是相同的类型，而不是类型（如 cd-rom 和 CD-R）的混合。

Microsoft 操作系统不支持写入一次光盘驱动器或更换有多种类型的驱动器。
