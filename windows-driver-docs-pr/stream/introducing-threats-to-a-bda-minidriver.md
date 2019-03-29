---
title: 引入对 BDA 微型驱动程序的威胁
description: 引入对 BDA 微型驱动程序的威胁
ms.assetid: 5dabf93a-9a85-4791-958c-59c8e0a99cf4
keywords:
- 广播驱动程序体系结构 WDK AVStream 安全性
- BDA WDK AVStream 安全性
- 安全 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b74d6b8c9fe74769e0fbed12a75f798023bbb4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562388"
---
# <a name="introducing-threats-to-a-bda-minidriver"></a>引入对 BDA 微型驱动程序的威胁





下面的路径可能是可以引入 BDA 微型驱动程序的威胁：

1.  信号传输流。

2.  特殊用途 Ioctl。

3.  直接 WDM 调度例程。

下图显示了可以如何引入 BDA 微型驱动程序的威胁：

![说明如何可以引入 bda 微型驱动程序的威胁的关系图](images/bdathret.png)

 

 




