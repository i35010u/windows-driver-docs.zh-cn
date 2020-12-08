---
title: 进程驻留预算
description: 在 Windows 显示器驱动程序模型 (WDDM) v2 中，会为进程分配预算，使其可以保持驻留的内存量。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b36daf5040698aecf569ffb991a4753727adcb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833041"
---
# <a name="process-residency-budgets"></a>进程驻留预算


在 Windows 显示器驱动程序模型 (WDDM) v2 中，会为进程分配预算，使其可以保持驻留的内存量。 此预算可能会随时间推移而变化，但通常仅当系统处于内存压力时才会受到影响。 在 Microsoft Direct3D 12 之前，将按用户模式驱动程序以 "*剪裁* 通知" 和 "**状态 \_ 无 \_ 内存**" *MakeResident* 失败的形式处理预算。 *TrimToBudget* Notification、[*逐出*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)和 failed [*MakeResident*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)调用都以整数 NumBytesToTrim 值的形式返回最新的预算，这是一个整数 **NumBytesToTrim** 值，它指示需要进行剪裁以适应新预算的量。

对于 Direct3D 12 应用程序，该应用程序将完全处理预算。 预算的大小旨在作为提示，让应用程序知道要如何调整其自身大小。 通过使用预算大小作为提示，应用程序可以决定要保留的资源数，以及要保留的资源的分辨率和质量。

为了正确管理这些预算，内核需要知道哪些内存应参与预算。 [**DXGK \_ SEGMENTFLAGS2**](./dxgk-segmentflags2.md)结构中有一个新的 **ApplicationTarget** 位，需要在内核模式驱动程序希望包含在预算逻辑中的段上进行设置。 例如，在离散的图形处理单元上 (GPU) 包含1段 VRAM，适用于应用程序的使用情况，并自动使用一段 VRAM 用于专用资源，驱动程序可能只会将主要 VRAM 段标记为 **ApplicationTarget**。 对于集成的 Gpu，主口径段通常会标记为。 对于可以标记为 **ApplicationTarget** 的段数没有限制。 内核将它们聚合在一起，并以统一的大小呈现应用程序。

 

