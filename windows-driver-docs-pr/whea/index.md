---
title: Windows 硬件错误体系结构 (WHEA) 设计指南
description: Windows 硬件错误体系结构 (WHEA) 设计指南
ms.assetid: 7a42bacd-cafe-48e0-8568-402738fd6e7c
keywords:
- Windows 硬件错误体系结构 WDK
- WHEA WDK
- 硬件错误 WDK WHEA
- 错误 WDK WHEA
- 检测硬件错误 WDK
- 报告硬件错误 WDK
- 从硬件错误中恢复 WDK WHEA
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 47fff24f4ff6d037d5492b3bb5a52fa857c54a6b
ms.sourcegitcommit: acef3c512676aad3aed1934cbe3d0f16e6d37619
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91372934"
---
# <a name="windows-hardware-error-architecture-whea-design-guide"></a>Windows 硬件错误体系结构 (WHEA) 设计指南

此部分介绍 Windows 硬件错误体系结构 (WHEA)，后者提供对硬件错误报告和恢复的支持。 此部分提供以下信息：

- WHEA 及其组件的概述。 有关详细信息，请参阅 [Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)。

- 如何开发和分发特定于平台的硬件错误驱动程序 (PSHED) 插件。有关详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

- 用户模式应用程序如何与 WHEA 平台通信。 有关详细信息，请参阅 [Windows 硬件错误体系结构感知型用户模式应用程序](windows-hardware-error-architecture-aware-user-mode-applications.md)。

## <a name="in-this-section"></a>本节内容

[Windows 硬件错误体系结构简介](introduction-to-the-windows-hardware-error-architecture.md)

[Windows 硬件错误体系结构的新信息](new-information-for-windows-hardware-error-architecture.md)

[Windows 硬件错误体系结构定义](windows-hardware-error-architecture-definitions.md)

[Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)

[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)

[Windows 硬件错误体系结构感知型用户模式应用程序](windows-hardware-error-architecture-aware-user-mode-applications.md)

[Windows 硬件错误体系结构调试程序扩展](windows-hardware-error-architecture-debugger-extensions.md)

## <a name="related-topics"></a>相关主题

[Windows 硬件错误体系结构 ACPI 表规范](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WHEA_ACPI-tables.docx)  

[Hardware Management and Security](/previous-versions/windows/hardware/design/dn614601(v=vs.85))（硬件管理和安全性）  

[**Bug 检查 0x124：WHEA\_UNCORRECTABLE\_ERROR（Windows 调试程序）** ](../debugger/bug-check-0x124---whea-uncorrectable-error.md)