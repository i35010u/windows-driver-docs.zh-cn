---
title: 处理 NDIS 端口状态指示
description: 处理 NDIS 端口状态指示
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- WDK NDIS，状态指示端口
- NDIS WDK，状态指示端口
- 状态指示 WDK 网络 NDIS 端口
- 端口状态 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa2736700309636b757f6c01e149a5ec037127f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347329"
---
# <a name="handling-ndis-ports-status-indications"></a>处理 NDIS 端口状态指示





如果 NDIS 端口的状态指示的源，应使用微型端口驱动程序**PortNumber**中的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构，以指定源端口。 微型端口驱动程序永远不会指示非活动状态的端口的状态。

微型端口驱动程序应使用[ **NDIS\_状态\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567415)状态指示，指示在 NDIS 端口的状态更改。 获取此状态指示，微型端口驱动程序必须设置的端口号**PortNumber**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 **StatusBuffer**成员的 NDIS\_状态\_指示结构包含一个指向[ **NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)结构。

 

 





