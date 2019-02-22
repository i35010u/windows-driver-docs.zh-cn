---
title: 添加驱动程序时考虑的要点
description: 添加驱动程序时考虑的要点
ms.assetid: bcbaa842-03b6-4311-9b93-1a4af165020b
keywords:
- WDM 驱动程序 WDK 内核配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 将驱动程序
- 添加内核模式驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c29a60fd6065c5bdd2048c69c24a273f168eb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554132"
---
# <a name="points-to-consider-when-adding-drivers"></a>添加驱动程序时考虑的要点





设计的内核模式驱动程序时，请记住以下几点：

-   无法替换系统提供的 SCSI 和视频端口驱动程序。

-   替换最低级别驱动程序必须实现与它将替换该驱动程序相同的功能。 例如，替换键盘或鼠标端口驱动程序必须使用自身的系统提供的类驱动程序，它重用之间的系统定义的接口，反之亦然。

-   新的中间驱动程序，插入系统提供的驱动程序，任何对之间必须与进行互操作这些驱动程序，以便不减少的上限和下限的驱动程序的功能。

 

 




