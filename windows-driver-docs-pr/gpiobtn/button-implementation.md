---
title: 按钮实现
description: 建议为按钮和状态指示器使用物理 GPIO 资源。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c4d71161f9e81ee461bafa2cc1550bc5169ed74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827173"
---
# <a name="button-implementation"></a>按钮实现


建议为按钮和状态指示器使用物理 GPIO 资源。

在没有必需/可选硬件按钮的物理 GPIO 资源的系统上，或者对于 GPIO 指示器 (便携式计算机/石板模式指示或停靠指示) ，用户模式或内核模式驱动程序可以将状态更改直接注入到收件箱驱动程序，而不是 (cid \_ PNP0C40) 、便携式计算机/石板模式状态指示器 (cid \_ PNP0C70 \_ (cid) 的物理硬件资源。) 

若要使用接口，ACPI 表中必须有一个条目，该项目定义了要使用接口的每个相应设备 (s) 。 不过，设备是否存在任何 GPIO 资源是可选的。 请参阅 [ACPI 描述符示例](acpi-descriptor-samples.md)。

 

 




