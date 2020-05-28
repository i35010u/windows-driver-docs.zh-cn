---
title: Windows UEFI 固件更新平台
description: Windows 支持通过使用 UpdateCapsule 函数处理的驱动程序包来安装系统和设备固件更新。
ms.assetid: 9F0D22FB-3C83-4F90-8E24-2205EEF9D5F7
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: e3c2c0e6398f6ba534e61209a1c6875ab59c622e
ms.sourcegitcommit: 5273e44c5c6c1c87952d74e95e5473c32a916d10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2020
ms.locfileid: "84122691"
---
# <a name="windows-uefi-firmware-update-platform"></a>Windows UEFI 固件更新平台

Windows 支持一个平台，用于通过使用 UEFI UpdateCapsule 函数处理的驱动程序包来安装系统和设备固件更新。 此平台提供一致、可靠的固件更新体验，并改善最终用户的重要系统固件更新的发现。

UEFI 固件更新平台指南适用于正在构建运行 Windows 的硬件平台的 SoC 供应商和 Oem。 以下操作系统版本支持 UEFI 固件更新平台：

- Windows 8
- Windows 8.1
- Windows 10 桌面版（家庭版、专业版、企业版和教育版）
- Windows 10 移动版

## <a name="uefi-firmware-update-support-in-windows-10"></a>Windows 10 中的 UEFI 固件更新支持

对于桌面版运行 Windows 10 的所有系统，都应遵循文档的本部分中所述的基于 UpdateCapsule 的更新过程来实现 UEFI 固件更新。

运行 Windows 10 移动版的设备可以遵循用于 Windows 10 桌面的基于 UpdateCapsule 的过程。 这些设备还可以遵循二进制更新过程，该过程对包含 UEFI 固件的存储分区执行二进制更新。

Microsoft 强烈建议运行 Windows 10 移动版的设备应使用二进制更新过程更新 UEFI 固件。 运行 Windows 10 移动版的设备只能在不能使用二进制更新过程的情况下使用基于 UpdateCapsule 的过程。 例如，如果设备的分区布局阻止 UEFI 固件通过使用二进制更新包进行更新，则为。

有关适用于 Windows 10 移动版的 spkg 包的详细信息，请参阅[创建包](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))和[更新](https://docs.microsoft.com/windows-hardware/service/mobile/index)。

## <a name="overview-of-the-uefi-firmware-update-platform"></a>UEFI 固件更新平台概述

可以通过 Windows 提供两种类型的固件：系统固件和设备固件。 系统固件负责为整个系统提供关键的启动和运行时服务，并且设备固件与集成到系统中的特定设备关联。 此类设备固件通常与设备驱动程序一起使用，从而使操作系统能够向操作系统级服务和应用程序公开设备。

### <a name="system-firmware-updates"></a>系统固件更新

基于 UEFI 的系统的系统固件更新将部署为设备驱动程序包（Inf）。 Windows 将使用平台提供的信息，以确保更新包仅适用于相应系统。 固件更新包包含包含系统固件映像的二进制文件。 固件更新包位于最终用户的系统上之后，Windows 将使用 UEFI UpdateCapsule 函数将固件负载移交给平台固件以进行处理。

将更新部署为驱动程序包可以使固件更新过程与许多现有的部署和服务工具保持一致，并确保为硬件供应商编写简单的更新包。

> [!NOTE]
> 固件更新作为驱动程序包提供的事实并不意味着将更新编写为实际的驱动程序。 驱动程序包将包含一个 INF 文件和一个包含系统或设备固件映像的二进制文件。

### <a name="device-firmware-updates"></a>设备固件更新

出于更新设备固件的目的，可以将设备固件分配给这两个类别之一：

- UEFI 可更新的设备固件。

    利用与系统固件相同的机制，可以使用设备驱动程序包更新此设备固件。 设备固件更新作为固件更新包分发。 固件更新包位于最终用户的系统上之后，Windows 将使用 UEFI UpdateCapsule 函数将设备固件负载移交给平台固件以进行处理。 此过程与 Windows 移交系统固件更新负载的方式几乎完全相同，如下所述。

    建议使用离散固件更新驱动程序包更新设备固件，但也可以使用系统固件更新设备固件，作为单一固件更新驱动程序包的一部分。

    **注意**   不应使用 UEFI 来更新外围设备。 UEFI 要求在重新启动过程中存在设备，以应用无法保证（外部、可移动）外围设备的固件更新。

- 驱动程序可更新的设备固件。

    此设备固件可以在正常 Windows OS 运行时中由设备驱动程序进行更新。 本文不包含使用普通 Windows OS 驱动程序更新设备固件的情况。

### <a name="system-requirements-for-windows-firmware-updates"></a>Windows 固件更新的系统要求

为了使系统与 Windows 固件更新机制兼容，它必须满足以下要求：

- 系统必须按照[UEFI 规范](https://uefi.org/specifications)的7.5.3 节中的定义来实现 UpdateCapsule 和 QueryCapsuleCapabilities。

    UpdateCapsule 用于通过 Windows 和平台固件传递固件更新负载。

- 平台固件必须支持 Windows 启动的固件更新。

    系统固件和某些设备固件类必须可使用此过程进行更新。 固件代码可识别传递给 UpdateCapsule 的固件更新有效负载，并启动更新过程。 该实现由合作伙伴拥有。

- 必须在 EFI 系统资源表（ESRT）中指定固件资源

    通过固件资源，Windows 可以通过硬件 ID （将用于将系统或设备固件更新定向到适当的系统和设备）来呈现设备实例。 它还描述当前固件版本，并提供以前更新的状态。

    系统固件更新存在单个条目。 具有可更新固件的所有设备都必须在 ESRT 中指定资源，除非设备的固件作为系统固件更新的一部分进行更新。

    有关详细信息，请参阅[ESRT 表定义](esrt-table-definition.md)。

## <a name="in-this-section"></a>在此部分中

- [通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)

- [实现对 UEFI 固件更新的支持](implementing-support-for-uefi-firmware-updates.md)

- [UEFI 固件更新的用户体验](user-experience-for-uefi-firmware-updates.md)
