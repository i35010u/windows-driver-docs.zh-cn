---
title: 扫描仪微驱动程序示例
description: 扫描仪微驱动程序示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ec2eb7b1045ad35fbeb2bde3cbb62832649a65c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794937"
---
# <a name="scanner-microdriver-sample"></a>扫描仪微驱动程序示例





WDK 中的 *microdrv* 目录包含扫描仪的示例 WIA microdriver。 与完整的 WIA 微型驱动程序相比，microdriver 的开发更容易，但只提供了基本的功能。 请参阅开发用于 microdriver 限制的 [WIA 扫描器驱动程序](developing-a-wia-scanner-driver.md) 。 此示例演示如何为平板扫描仪编写 WIA microdriver。 此示例驱动程序可用作开发的起点，但驱动程序应通过 Windows 提供的一个内核模式驱动程序来访问扫描程序硬件。

 

 




