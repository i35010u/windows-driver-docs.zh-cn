---
title: 适用于 Windows 7 配置系统固件并启用适用于 Windows 10
description: 适用于 Windows 7 配置系统固件并启用适用于 Windows 10
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07b9db4b912514d09a91e1ed415e1ad1c8ebf626
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328079"
---
# <a name="configure-system-firmware-for-windows-7-and-enable-for-windows-10"></a>适用于 Windows 7 配置系统固件并启用适用于 Windows 10


若要设置新式系统安装的下层操作系统 （如 Windows 7)，可以使用此清单以满足 Windows 7 和 Windows 10 的要求。

- 配有 UEFI 2.3.1 勘误表 C;这基于一项要求 Windows 8.1 为预期的未来升级到 Windows 10。

- 安全引导组件，应为 Windows 10 安装 （证书等）请参阅[安全引导](secure-boot.md)有关详细信息。

- 用于 Windows 7 中的 TPM 支持 TPM 2.0。 请参阅[KB2920188](https://support.microsoft.com/kb/2920188)有关详细信息。

- 系统和设备，可以更新固件，EFI 系统资源 Table(ESRT) 应填充了特定的模型的唯一 ID。

- **UpdateCapsule()** 并**QueryCapsuleCapabilitiesenabled()** 在 UEFI 中。

- SMBIOS 配置和填充每个[SMBIOS](smbios.md)指南 （即使使用下层 SMBIOS，合理范围内的）。

- CSM 已启用。 这所需的 Windows 7，将禁用安全启动。

- 将硬盘驱动器配置为 GPT 磁盘。

- 有关 UEFI 引导配置的设备。

**请注意**这些要求基于 Windows 7 要求，如启用了 UEFI 引导 CSM 和 Windows 10 的要求，如 ESRT 并**UpdateCapsule()** 正在启用。


