---
title: 引入对 BDA 微型驱动程序的威胁
description: 引入对 BDA 微型驱动程序的威胁
keywords:
- 广播驱动程序体系结构 WDK AVStream，安全性
- BDA WDK AVStream，安全性
- 安全 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d559c8789125fad4ff773882a8ecf5a0ff5faa4a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790269"
---
# <a name="introducing-threats-to-a-bda-minidriver"></a>引入对 BDA 微型驱动程序的威胁





以下路径可能会引入 BDA 微型驱动程序威胁：

1.  信号传输流。

2.  专用 IOCTLs。

3.  直接 WDM 调度例程。

下图显示了如何引入 BDA 微型驱动程序威胁：

![说明如何引入 bda 微型驱动程序威胁的示意图](images/bdathret.png)

 

 




