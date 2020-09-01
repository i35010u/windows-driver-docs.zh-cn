---
title: 禁用帧指针省略 (FPO) 优化
description: 在 Windows 7 中，Windows 显示驱动程序模型 (WDDM) 1.1 内核模式驱动程序需要禁用帧指针省略 (FPO) 优化，以提高诊断性能问题的能力。
ms.assetid: ABA1A097-D9AA-41F4-90D4-B2FBB9B08534
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92423a8c59bb6c5affc38a70b1dfb0fb421f638d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067440"
---
# <a name="disabling-frame-pointer-omission-fpo-optimization"></a>禁用帧指针省略 (FPO) 优化


在 Windows 7 中，Windows 显示驱动程序模型 (WDDM) 1.1 内核模式驱动程序需要禁用帧指针省略 (FPO) 优化，以提高诊断性能问题的能力。 从 Windows 8 开始，相同的要求适用于所有 WDDM 1.2 及更高版本的驱动程序 (用户模式和内核模式) ，从而更容易调试与字段中的 FPO 相关的性能问题。

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现：完整图形、仅呈现和显示**：必需

** [WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**：[内核视频驱动程序的 WHQL FPO 优化检查](/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2)


 

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅[内核视频驱动程序的 WHQL FPO 优化检查](/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2)相关的[WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit)。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

