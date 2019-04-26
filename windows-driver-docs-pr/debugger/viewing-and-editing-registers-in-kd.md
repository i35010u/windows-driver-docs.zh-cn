---
title: 在 KD 中查看和编辑寄存器
description: KD，可以查看和编辑寄存器输入 r （寄存器） 命令。 使用多个选项或使用 rm （注册掩码） 命令，可以自定义显示。
ms.assetid: 42306338-6E11-4724-B62F-D1E0BDBA7F8D
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef4589d8237dee7308f168cf4ff534850800013
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326005"
---
# <a name="viewing-and-editing-registers-in-kd"></a>在 KD 中查看和编辑寄存器


寄存器是位于在 CPU 的小易失性内存单位。 许多寄存器专用于特定用途，并可用于用户模式应用程序使用的其他寄存器。 基于 x86 和基于 x64 的处理器在有可用的寄存器的不同集合。 在每个处理器寄存器的详细信息，请参阅[处理器体系结构](processor-architecture.md)。

KD，您可以查看和编辑通过输入寄存器[ **r （寄存器）** ](r--registers-.md)命令。 可以使用多个选项或使用自定义显示[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

寄存器也会自动显示每个目标停止的时间。 如果在逐句通过代码[ **p （步骤）** ](p--step-.md)或[ **t (Trace)** ](t--trace-.md)命令，你将看到一个函数注册表，显示每个步骤。 若要停止此显示，请使用**r**选项时使用这些命令。

在基于 x86 的处理器上， **r**选项还可以控制多个名为标志的一位寄存器。 若要更改这些标志，您可以使用比时更改常规寄存器略有不同的语法。 有关这些标志和此语法的说明的详细信息，请参阅[x86 标志](x86-architecture.md#x86-flags)。

 

 





