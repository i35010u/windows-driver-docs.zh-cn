---
title: 固件更新
description: 介绍用于传递使用 Microsoft Windows Update (WU) 和 UEFI UpdateCapsule 函数的系统和设备固件更新的支持。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2d65fe0c7ee496e9d75d2d3d90fac93c9bbc8b50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337608"
---
# <a name="firmware-update"></a>固件更新

Windows 支持一个平台，用于提供系统和设备固件更新包装在使用 Microsoft Windows Update (WU) 提供的驱动程序包然后交给并在 UEFI 中处理**UpdateCapsule**函数. 此平台提供一致、 可靠的固件更新体验，并改进了将固件更新为最终用户提供重要的系统的功能。

尽早为 Windows 8.1 已提供此功能。 但是，某些最新的更改需要固件提供程序组合模型以及目标计算机的硬件 ID (CHID) 唯一 EFI 系统资源表 (ESRT) UEFI\_RES\\{唯一 ID} 更准确地目标特定系统或系统的范围。

ESRT 中的唯一 ID {唯一 ID} 至关重要。 唯一 ID + CHID 目的是使固件提供程序将能够创建固件更新包/BIOS 将对与 UNIQUE ID + CHID 相匹配的所有系统部署通过 Windows Update (WU)。 Microsoft 不具有一种机制来验证固件包，以及什么依赖于固件提供程序 （包的创建者） 来验证有效负载不被篡改。 它应通过密码验证;校验和或其他 Crc 不验证。 如果负载未通过验证它应失败并记录在 ESRT 的状态，如中所述[ESRT 表定义](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)。

> [!NOTE]
> 如果发现 ESRT 已预先填充 {唯一 ID} OEM、 ODM 或执行任务的填充 ESRT {唯一 ID} 的人员，不要假定这是唯一。 填充与你的 {唯一 ID} ESRT 并将它保存以供将来使用。 Microsoft 有有关如何创建一个唯一 ID，对于这些方案的指南。 本指南的可下载文档中适用[驱动程序发布工作流适用于 Windows 10](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)。



## <a name="in-this-section"></a>本节内容

[生成并提交固件包到 Windows Update (WU)](build-and-submit-a-firmware-package-to-windows-update.md)

[面向使用 CHID 的系统](target-a-system-using-chid.md)

[固件用户体验 (UX) 最佳实践](firmware-user-experience-best-practices.md)

[固件更新验证测试](firmware-update-validation-testing.md)






