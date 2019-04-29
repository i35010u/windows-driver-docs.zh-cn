---
title: 按钮实现
description: 我们建议用于按钮和状态指示器的物理 GPIO 资源。
ms.assetid: ECF0723A-1AF0-4608-88CC-6ACBD98DA03C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d77ef895fd5ed00f5b29736fc9edd563e16d80e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326108"
---
# <a name="button-implementation"></a>按钮实现


我们建议用于按钮和状态指示器的物理 GPIO 资源。

在系统上不具有物理 GPIO 资源必需/可选硬件按钮或用于 GPIO 的指示符 （便携式计算机/盖板模式指示或停靠的指示），一个用户模式或内核模式驱动程序可以注入到收件箱驱动程序而不是直接状态更改归属于按钮数组设备的物理硬件资源 (\_CID PNP0C40)，便携式计算机/盖板模式状态指示器 (\_CID PNP0C60) 或停靠状态指示器 (\_CID PNP0C70)。

若要使用一个接口，定义每个接口旨在利用相应设备的 ACPI 表中必须存在的条目。 但是，存在的任何 GPIO 资源的设备是可选的。 请参阅[ACPI 描述符示例](acpi-descriptor-samples.md)。

 

 




