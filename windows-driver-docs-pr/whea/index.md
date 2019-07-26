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
author: EliotSeattle
ms.openlocfilehash: 9614a4c05281277c7e3611338c320935f7b55f8b
ms.sourcegitcommit: 85d02ecf7cbcfd802f41f68cea4cd4434284bdaa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68473539"
---
# <a name="windows-hardware-error-architecture-whea-design-guide"></a>Windows 硬件错误体系结构 (WHEA) 设计指南

此部分介绍 Windows 硬件错误体系结构 (WHEA)，后者提供对硬件错误报告和恢复的支持。 此部分提供以下信息：

- WHEA 及其组件的概述。 有关详细信息，请参阅 [Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)。

- 如何开发和分发特定于平台的硬件错误驱动程序 (PSHED) 插件。有关详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

- 用户模式应用程序如何与 WHEA 平台通信。 有关详细信息，请参阅 [Windows 硬件错误体系结构感知型用户模式应用程序](windows-hardware-error-architecture-aware-user-mode-applications.md)。

若要更详细地了解 WHEA 以及如何在硬件平台上实现 WHEA，请参阅“WHEA 平台设计指南”。 平台供应商可以通过向 <wheafb@microsoft.com> 发送电子邮件获取此设计指南。

> [!NOTE]
> Windows Vista、Windows Server 2008 以及更高版本的 Windows 操作系统支持 WHEA。 有关硬件错误报告（在 Windows Vista 之前的 Microsoft Windows 版本上支持），请参阅[计算机检查体系结构 (MCA)](https://docs.microsoft.com/previous-versions/windows/hardware/mca/ff540685(v=vs.85))。

## <a name="in-this-section"></a>本部分内容

[Windows 硬件错误体系结构简介](introduction-to-the-windows-hardware-error-architecture.md)

[Windows 硬件错误体系结构的新信息](new-information-for-windows-hardware-error-architecture.md)

[Windows 硬件错误体系结构定义](windows-hardware-error-architecture-definitions.md)

[Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)

[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)

[Windows 硬件错误体系结构感知型用户模式应用程序](windows-hardware-error-architecture-aware-user-mode-applications.md)

[Windows 硬件错误体系结构调试程序扩展](windows-hardware-error-architecture-debugger-extensions.md)

## <a name="related-topics"></a>相关主题

[Windows 硬件错误体系结构 ACPI 表规范](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WHEA_ACPI-tables.docx)  

[Hardware Management and Security](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614601(v=vs.85))（硬件管理和安全性）  

[**Bug 检查 0x124：WHEA\_UNCORRECTABLE\_ERROR（Windows 调试程序）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x124---whea-uncorrectable-error)  
