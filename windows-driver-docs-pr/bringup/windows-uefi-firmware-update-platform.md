---
title: Windows UEFI 固件更新平台
description: Windows 支持通过使用 UpdateCapsule 函数进行处理的驱动程序包安装系统和设备固件更新。
ms.assetid: 9F0D22FB-3C83-4F90-8E24-2205EEF9D5F7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82190d7efe9a28700310df7a188f391618ba6c20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575265"
---
# <a name="windows-uefi-firmware-update-platform"></a>Windows UEFI 固件更新平台


Windows 支持一个平台，用于安装系统和通过使用 UEFI UpdateCapsule 函数处理的驱动程序包的设备固件更新。 此平台提供一致、 可靠的固件更新体验，并改进了重要的系统固件更新为最终用户的可发现性。

UEFI 固件更新平台指南适用于 SoC 供应商和 Oem 负责构建运行 Windows 的硬件平台。 UEFI 固件更新平台支持以下操作系统版本：

-   Windows 8
-   Windows 8.1
-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

## <a name="uefi-firmware-update-support-in-windows-10"></a>Windows 10 中的 UEFI 固件更新支持


运行 Windows 10 桌面版的所有系统应按照在文档的此部分中所述的基于 UpdateCapsule 的更新过程中都实现 UEFI 固件更新。

运行 Windows 10 移动版的设备可以按照用于 Windows 10 桌面版基于 UpdateCapsule 的过程。 这些设备也可以按照二进制更新过程中，执行的存储分区，其中包含 UEFI 固件的一个二进制更新。

Microsoft 强烈建议运行 Windows 10 移动版的设备应使用二进制更新过程中更新 UEFI 固件。 运行 Windows 10 移动版的设备可以使用基于 UpdateCapsule 的过程仅在方案中无法使用二进制更新过程的。 例如，如果设备的分区布局阻止 UEFI 固件更新使用二进制更新包。

对于 Windows 10 移动版.spkg 程序包的详细信息，请参阅[创建包](https://msdn.microsoft.com/library/dn756642)并[更新](https://msdn.microsoft.com/library/dn757518)。

## <a name="overview-of-the-uefi-firmware-update-platform"></a>UEFI 固件更新平台概述


有两种类型的固件，可以通过 Windows 提供服务： 系统固件和设备固件。 系统固件负责提供关键启动和运行时服务作为一个整体系统和设备固件是关联与特定设备集成到系统。 此类设备固件通常一起使用的设备驱动程序，允许操作系统公开 OS 级服务和应用程序到设备。

### <a name="system-firmware-updates"></a>系统固件更新

将设备驱动程序包 (Inf) 作为部署的基于 UEFI 的系统的系统固件更新。 Windows 将使用平台提供的信息以确保更新包仅适用于相应的系统。 固件更新包包含包含系统固件映像的二进制文件。 最终用户的系统上的固件更新包后，Windows 将使用 UEFI UpdateCapsule 函数以提交固件有效负载为平台固件进行处理。

部署驱动程序包的更新使固件更新过程，以便与许多现有的部署和维护工具，保持一致，并确保为硬件供应商编写的简单的更新包。

**请注意**  发送固件更新，因为驱动程序包并不意味着该更新将被写入作为实际的驱动程序这一事实。 驱动程序包将包含一个 INF 文件和包含系统或设备的固件映像的二进制文件。

 

### <a name="device-firmware-updates"></a>设备固件更新

为了更新设备固件，可以将设备固件分配给这两个类别之一：

-   UEFI 可更新设备固件。

    可以使用设备驱动程序包利用相同的机制系统固件更新此设备固件。 设备固件更新是作为固件更新包分发的。 最终用户的系统上的固件更新包后，Windows 将使用 UEFI UpdateCapsule 函数以提交设备固件负载对平台固件进行处理。 此过程与 Windows 如何关闭系统固件更新有效负载，几乎相同，下面将讨论。

    此外，建议设备固件更新使用离散固件更新驱动程序包，但设备固件可能还会更新系统固件与单个固件更新驱动程序包的一部分。

    **请注意**  UEFI 不应该用于更新外围设备。 UEFI 要求设备必须重启以应用不能保证与 （外部，可移动） 的外围设备的固件更新期间存在。

     

-   驱动程序可更新设备固件。

    在正常的 Windows 操作系统运行时，可以通过设备驱动程序更新此设备固件。 本文未涵盖更新设备固件使用正常的 Windows 操作系统驱动程序。

### <a name="system-requirements-for-windows-firmware-updates"></a>Windows 固件更新的系统要求

为了使系统能够兼容 Windows 固件更新机制，它必须满足以下要求：

-   系统必须实现 UpdateCapsule 和 QueryCapsuleCapabilities 定义的部分的 7.5.3 [UEFI 规范](https://go.microsoft.com/fwlink/p/?LinkId=218221)。

    UpdateCapsule 用于 Windows 和平台固件之间传递的固件更新有效负载。

-   平台固件必须支持由 Windows 启动固件更新。

    系统固件和设备固件的某些类必须是可更新使用此过程。 固件代码识别传递给 UpdateCapsule 的固件更新有效负载，并启动更新过程。 实现属于合作伙伴。

-   必须指定固件资源在 EFI 系统资源表 (ESRT)

    固件资源允许 Windows 来呈现使用硬件 ID 将用于目标系统或设备固件更新到相应的系统和设备的设备实例。 它还描述当前固件版本并提供以前的更新的状态。

    存在对系统固件更新单个条目。 使用可更新固件的所有设备必须都具有 ESRT 中指定的资源，除非设备的固件更新作为系统固件更新的一部分。

    有关详细信息，请参阅[ESRT 表定义](esrt-table-definition.md)。

## <a name="in-this-section"></a>本节内容


-   [通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)
-   [实现对 UEFI 固件更新的支持](implementing-support-for-uefi-firmware-updates.md)
-   [用户体验的 UEFI 固件更新](user-experience-for-uefi-firmware-updates.md)

 

 




