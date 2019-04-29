---
title: 在 Windows 中启用 PCI Express 原生控制
description: PCI Express 的功能，可通过在 Windows 中 PCI Express 本机控件功能控制
ms:assetid: 0E3A4408-CBF7-494F-9F25-7C78E04526B4
keywords: ACPI、 ACPI \_OSC 方法
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6d3572482779b7b0db40bd1e6936fb59034a88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379761"
---
# <a name="enabling-pci-express-native-control-in-windows"></a>在 Windows 中启用 PCI Express 原生控制

高级配置和电源接口 (ACPI) 操作系统功能 (\_OSC) 方法用于通信的功能或可由操作系统控制平台中提供的功能。 ACPI 规范，修订版本 4.0 中定义此方法。

下表列出了可通过在 Windows Vista、 Windows Server 2008 和更高版本的 Windows 中 PCI Express 本机控件功能控制的 PCI Express 的功能。 这些功能在 PCI Express Base 规范中定义并由操作系统通过 ACPI 控制\_OSC 方法。

| PCI 速成版功能                        | PCI Express Native Control |
| ------------------------------------------ | -------------------------- |
| PCI Express 本机热插拔                | 强制                  |
| PCI Express 本机电源管理事件 | 强制                  |
| PCI Express 高级错误报告       | 可选                   |
| PCI Express 功能结构控制   | 强制                  |

如果\_OSC 方法授予到操作系统，这些功能控制 Windows 启用 PCI 高速本机控制功能。 在 Windows 中的 PCI Express 本机控件功能不依赖上 PCI Express 高级错误报告 (AER)，并因此 PCI Express AER 的平台支持是可选的。

如果该平台不实现\_OSC 方法，或者如果\_OSC 方法进行通信的任何表中列出的 PCI Express 功能操作系统控制不可用，因此不会授予的强制性控制上述操作系统的功能，然后 Windows 不会启用任何通过 PCI Express 本机控件 PCI Express 的高级功能。

有关详细信息，请参阅部分 6.2.10 ACPI 规范、 修订版本 4.0 和 4.5 PCI 固件规范中的节。

在 ACPI 和 PCI SIG Web 站点上提供了这些规范：

  - [ACPI 网站](https://www.uefi.org/specifications)
  - [PCI SIG 网站](http://www.pcisig.org/)

## <a name="see-also"></a>请参阅
[PCIe 根端口的设备特定数据 (_DSD)](dsd-for-pcie-root-ports.md)
