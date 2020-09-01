---
title: 固件更新
description: 描述支持使用 Microsoft Windows 更新 ( WU) 和 UEFI UpdateCapsule 函数来传送系统和设备固件更新。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: aa01b0042e4ef669eb34aa7f213a1dabc58b7eed
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187643"
---
# <a name="firmware-update"></a>固件更新

Windows 支持一个平台，用于传递使用 Microsoft Windows 更新 (WU) 传递的驱动程序包中包装的系统和设备固件更新，并在 UEFI **UpdateCapsule** 函数中移交并进行处理。 此平台提供一致、可靠的固件更新体验，并改善为最终用户提供重要系统固件更新的能力。

此功能现已提供 Windows 8.1。 但是，某些最近的更改要求固件提供程序将计算机硬件 ID (子) 目标与模型唯一的 EFI 系统资源表结合使用， (ESRT) UEFI \_ RES \\ {unique ID}，以更准确地确定特定系统或系统范围。

ESRT 中的唯一 ID {UNIQUE ID} 很重要。 唯一 ID + 子的目的在于，固件提供程序将能够创建固件更新包/BIOS，该固件更新包/BIOS 将通过 Windows 更新 (WU) 部署到与唯一 ID + 子匹配的所有系统。 Microsoft 没有验证固件包的机制，它依赖于固件提供程序 (包) 的创建者，以验证负载是否未被篡改。 它应经过密码验证;校验和或其他 CRCs 不是验证。 如果负载失败，则它应失败并记录 ESRT 中的状态，如 [ESRT 表定义](./esrt-table-definition.md)中所述。

> [!NOTE]
> 如果用来填充 ESRT {唯一 ID} 的 OEM、ODM 或人员发现 ESRT 是使用 {Unique ID} 预填充的，请不要认为这是唯一的。 使用 {唯一 ID} 填充 ESRT，并记录此情况以供以后使用。 对于这些方案，Microsoft 提供了有关如何创建唯一 ID 的指导。 本指南位于适用于 [Windows 10 的驱动程序发布工作流](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)的可下载文档中。

## <a name="in-this-section"></a>本节内容

[生成固件包并将其提交到 Windows 更新 (WU)](build-and-submit-a-firmware-package-to-windows-update.md)

[面向使用 CHID 的系统](target-a-system-using-chid.md)

[固件用户体验 (UX) 最佳做法](firmware-user-experience-best-practices.md)

[固件更新验证测试](firmware-update-validation-testing.md)