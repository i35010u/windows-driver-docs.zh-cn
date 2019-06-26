---
title: 进程驻留预算
description: 在 Windows 显示驱动程序模型 (WDDM) v2 中，进程将分配的内存量保持常驻的预算。
ms.assetid: 9A93E110-4D3F-4D08-8379-222A2D7DEFBB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774f0fd2a8a04dd7de35d3228d68efa76c0b349a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363708"
---
# <a name="process-residency-budgets"></a>进程驻留预算


在 Windows 显示驱动程序模型 (WDDM) v2 中，进程将分配的内存量保持常驻的预算。 此预算随着时间推移，可以更改，但通常仅施加时系统处于内存压力下。 在 Microsoft Direct3D 12 中之前, 预算处理的窗体中的用户模式驱动程序通过*剪裁*通知并*MakeResident*具有失败**状态\_没有\_内存**。 *TrimToBudget*通知[*逐出*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)，和失败[ *MakeResident* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)所有调用将都返回在最新的预算窗体的一个整数**NumBytesToTrim**值，该值指示多大需要进行剪裁以适应新的预算。

对于 Direct3D 12 应用程序，由应用程序完全处理预算。 预算的大小作为一个提示用于允许应用程序知道要调整到自身的内容。 通过使用预算大小作为提示，应用程序可以决定要保留驻留、 哪些分辨率和质量的资源要保留的资源数量。

若要正确地管理这些预算，需要知道哪些内存应参与预算内核。 新增了一个**ApplicationTarget**位[ **DXGK\_SEGMENTFLAGS2** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-segmentflags2)需要在内核模式驱动程序想要的段上设置的结构包含在预算方面的逻辑。 例如，1 个段的 vram 能够与离散图形处理单元 (GPU) 上的适用于应用程序使用情况和 1 个段的 vram 能够使用专用的资源自动，驱动程序将可能仅标记主 vram 能够段作为**ApplicationTarget**。 为集成 Gpu 主要 aperture 段通常是一个标记。 可以将多少段标记为无限制**ApplicationTarget**。 内核将聚合到一起，并提供统一的大小与应用程序。

 

 





