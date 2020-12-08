---
title: 添加驱动程序时要考虑的要点
description: 添加驱动程序时要考虑的要点
keywords:
- WDM 驱动程序 WDK 内核，配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 替换驱动程序
- 添加内核模式驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c919aa505212a4ad2e988d586cb2cea4169c9afd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822305"
---
# <a name="points-to-consider-when-adding-drivers"></a>添加驱动程序时要考虑的要点





设计内核模式驱动程序时，请记住以下几点：

-   无法更换系统提供的 SCSI 和视频端口驱动程序。

-   替换最低级别驱动程序必须实现与它所替换的驱动程序相同的功能。 例如，替换键盘或鼠标端口驱动程序必须在自身与系统提供的类驱动程序之间使用系统定义的接口，反之亦然。

-   在任何系统提供的驱动程序对之间插入的新中间驱动程序必须与这些驱动程序进行互操作，以便不会降低上层驱动程序的功能。

 

 




