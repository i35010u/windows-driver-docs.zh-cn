---
title: 禁用帧指针省略 (FPO) 优化
description: 在 Windows 7 中，Windows 显示驱动程序模型 (WDDM) 1.1 内核模式驱动程序所需禁用框架指针省略 (FPO) 优化，以提高诊断性能问题的能力。
ms.assetid: ABA1A097-D9AA-41F4-90D4-B2FBB9B08534
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a7ac0ce1a713890191b74b55cdecd7734a2a9cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358919"
---
# <a name="disabling-frame-pointer-omission-fpo-optimization"></a>禁用帧指针省略 (FPO) 优化


在 Windows 7 中，Windows 显示驱动程序模型 (WDDM) 1.1 内核模式驱动程序所需禁用框架指针省略 (FPO) 优化，以提高诊断性能问题的能力。 从 Windows 8 开始，相同的要求是适用于所有 WDDM 1.2 和更高版本的驱动程序 （用户模式和内核模式下），从而更轻松地调试性能问题与 FPO 字段中。

|                                                                                   |                                                                                    |
|-----------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| WDDM 的最低版本                                                              | 1.2                                                                                |
| 最大 Windows 版本                                                           | 8                                                                                  |
| 驱动程序实现，所有的图形呈现，并仅显示                | 强制                                                                          |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | [WHQL FPO 优化检查内核视频驱动程序](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2) |

 

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上[内核视频驱动程序的 WHQL FPO 优化检查](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2)。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





