---
title: 在 CDB 中查看和编辑寄存器
description: 在 CDB 中，可以通过在调试器命令窗口中输入 r (寄存器) 命令来查看寄存器。 您可以使用多个选项或通过使用 rm (注册掩码) 命令自定义显示。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 894f03629391d01f208bfa89b498f457ceb82fd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787717"
---
# <a name="viewing-and-editing-registers-in-cdb"></a>在 CDB 中查看和编辑寄存器


寄存器是位于 CPU 上的小型易失性内存单元。 许多注册专用于特定用途，其他寄存器可供用户模式应用程序使用。 基于 x86 和基于 x64 的处理器具有不同的可用寄存器集合。 有关每个处理器上寄存器的详细信息，请参阅 [处理器体系结构](processor-architecture.md)。

在 CDB 中，可以通过在调试器命令窗口中输入 [**r (寄存器)**](r--registers-.md) 命令来查看寄存器。 您可以使用多个选项或通过使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令自定义显示。

每次目标停止时，也会自动显示寄存器。 如果你使用 [**p (步骤)**](p--step-.md) 或 [**t (Trace)**](t--trace-.md) 命令单步执行代码，则会看到每个步骤的寄存器显示。 若要停止此显示，请在使用这些命令时使用 **r** 选项。

在基于 x86 的处理器上， **r** 选项还控制多个称为标志的一位寄存器。 若要更改这些标志，使用的语法略有不同。 有关这些标志的详细信息以及此语法的说明，请参阅 [X86 标志](x86-architecture.md#x86-flags)。

 

 





