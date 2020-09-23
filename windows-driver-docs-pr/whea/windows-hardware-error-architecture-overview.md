---
title: Windows 硬件错误体系结构概述
description: Windows 硬件错误体系结构概述
ms.assetid: 859caa70-371c-4191-baf9-52a38411164a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 41854d10418336761aa43f5c0ef5a4659e37643f
ms.sourcegitcommit: 1535a9ac3ec390340bb3c7e7bed9ac08ba1d2bdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007424"
---
# <a name="windows-hardware-error-architecture-overview"></a>Windows 硬件错误体系结构概述

Windows 10 版本 1903 包含 WHEA 的简化界面。  有关详细信息，请参阅以下页：

- [**WheaAddErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
- [**WheaReportHwErrorDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
- [**WheaRemoveErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
- [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
- [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
- [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

本节包括下列主题：

[硬件错误和错误源](hardware-errors-and-error-sources.md)

[Microsoft Windows 和系统固件之间的关系](relationship-between-microsoft-windows-and-the-system-firmware.md)

[Windows 硬件错误体系结构的组件](components-of-the-windows-hardware-error-architecture.md)

[错误处理](error-processing.md)

[错误记录](error-records.md)

[错误记录持久性机制](error-record-persistence-mechanism.md)

[预计故障分析 (PFA)](predictive-failure-analysis--pfa-.md)

[与早期版本的 Microsoft Windows 的差异](differences-from-previous-versions-of-microsoft-windows.md)

 

