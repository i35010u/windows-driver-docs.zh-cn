---
title: 更改浮点控制状态
description: 更改浮点控制状态
keywords:
- 浮点控制状态 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c97f829538f259db70918043bc953c8307e5766
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810329"
---
# <a name="changing-floating-point-control-state"></a>更改浮点控制状态


显示微型端口驱动程序和用户模式显示驱动程序的所有功能必须先保存浮点控件状态（如、舍入模式或精度），然后才能更改浮点控件状态，并且在返回之前必须将浮点控件状态还原到以前保存的设置。

 

 





