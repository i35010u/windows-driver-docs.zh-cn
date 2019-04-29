---
title: Windows 硬件错误体系结构概述
description: Windows 硬件错误体系结构概述
ms.assetid: 859caa70-371c-4191-baf9-52a38411164a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bfeb0802333e7e3f1393be049dad71b98e8111d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323135"
---
# <a name="windows-hardware-error-architecture-overview"></a>Windows 硬件错误体系结构概述

Windows 10 版本 1903年包括 WHEA 的简化的界面。  有关详细信息，请参阅以下页面：

- [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
- [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
- [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
- [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
- [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
- [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
- [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

本部分包括以下主题：

[硬件错误和错误源](hardware-errors-and-error-sources.md)

[Microsoft Windows 和系统固件之间的关系](relationship-between-microsoft-windows-and-the-system-firmware.md)

[Windows 硬件错误体系结构的组件](components-of-the-windows-hardware-error-architecture.md)

[错误处理](error-processing.md)

[错误记录](error-records.md)

[错误记录持久性机制](error-record-persistence-mechanism.md)

[预计故障分析 (PFA)](predictive-failure-analysis--pfa-.md)

[从早期版本的 Microsoft Windows 的差异](differences-from-previous-versions-of-microsoft-windows.md)

 

 




