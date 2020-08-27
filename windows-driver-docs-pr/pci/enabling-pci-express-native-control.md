---
title: 在 Windows 中启用 PCI Express 原生控制
description: 可由 Windows 中的 PCI Express 本机控制功能控制的 PCI Express 功能
ms:assetid: 0E3A4408-CBF7-494F-9F25-7C78E04526B4
keywords: ACPI，ACPI \_ .osc 方法
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f40e57d4870f8cf1cdf32536ab658d62cde75a6
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902566"
---
# <a name="enabling-pci-express-native-control-in-windows"></a>在 Windows 中启用 PCI Express 原生控制

高级配置和电源接口 (的 ACPI) 操作系统功能 (\_ .osc) 方法用于传达平台中提供的哪些功能或功能可以由操作系统控制。 此方法在 ACPI 规范版本4.0 中定义。

下表列出了可通过 Windows Vista、Windows Server 2008 和更高版本的 Windows 中的 PCI Express 本机控制功能控制的 PCI Express 功能。 这些功能是在 PCI Express 基本规范中定义的，由操作系统通过 ACPI \_ .osc 方法控制。

| PCI Express 功能                        | PCI Express 本机控件 |
| ------------------------------------------ | -------------------------- |
| PCI Express 本机热插拔                | 必需                  |
| PCI Express 本机电源管理事件 | 必需                  |
| PCI Express 高级错误报告       | 可选                   |
| PCI Express 功能结构控件   | 必需                  |

如果 \_ .osc 方法将对这些功能的控制权限授予操作系统，Windows 将启用 PCI Express 本机控制功能。 Windows 中的 PCI Express 本机控制功能不依赖于 PCI Express 高级错误报告 (AER) ，因此，PCI Express AER 的平台支持是可选的。

如果平台未实现 \_ .osc 方法，或者如果 \_ .osc 方法传达该表中列出的任何 PCI Express 功能的操作系统控制不可用，因此它不会将上述必需功能的控制权限授予操作系统，则 Windows 将不会通过 PCI Express 本机控件启用任何高级 PCI express 功能。

有关详细信息，请参阅6.2.10 中的 "ACPI 规范"、修订版4.0 和第4.5 节中的部分。

ACPI 和 PCI SIG 网站上提供了这些规范：

- [ACPI 网站](https://uefi.org/specifications)
- [PCI SIG 网站](https://pcisig.com/)

## <a name="see-also"></a>另请参阅

[PCIe 根端口的设备特定数据 (_DSD)](dsd-for-pcie-root-ports.md)
