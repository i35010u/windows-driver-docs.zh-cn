---
title: 在 Windows 10 上使用 WHEA
description: 介绍如何在 Windows 10 上报告 WHEA 错误
keywords:
- Windows 硬件错误体系结构 WDK，Windows 10 更改
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9cc3a1542b66b8902042e065eb2ec816c4306b7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820423"
---
# <a name="using-whea-on-windows-10"></a>在 Windows 10 上使用 WHEA

在 Windows 10 中，版本2004，Windows 硬件错误体系结构 (WHEA) 包括 (v2) 的新接口。  本页介绍如何将作为错误源进行注册并报告错误。

## <a name="adding-an-error-source"></a>添加错误源

若要使用 WHEA v2 注册 WHEA 作为错误源，驱动程序应执行以下操作：

1. 通过实例化 [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver) 结构来指定设备驱动程序的配置，并提供指向 [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver) 和 [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver) 事件回调函数的指针。
2. 调用 [**WheaAddErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)，提供配置结构。  通常，驱动程序从 *DriverEntry* 调用此例程。

    若要以后删除错误源，请调用 [**WheaRemoveErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)。

3. 当错误源准备好报告错误时，WHEA 将调用驱动程序的 [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver) 事件回调函数。 驱动程序接收 *ErrorSourceId* 作为回调的参数。

## <a name="reporting-an-error"></a>报告错误

若要报告错误，请同时按顺序执行以下步骤：

1. 调用 [**WheaCreateHwErrorReportDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheacreatehwerrorreportdevicedriver)，并为驱动程序提供 *ErrorSourceId* 和 *DeviceObject* 。  例程返回正在进行的错误的句柄。

2. 若要将数据添加到错误，请调用 [**WheaAddHwErrorReportSectionDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaaddhwerrorreportsectiondevicedriver)，提供错误句柄。  此函数向错误报告添加单个部分，并配置驱动程序提供的数据缓冲区。  驱动程序可调用此例程，最多可调用 [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)中指定的 **MaxSectionsPerReport** 时间。

    或者，驱动程序可以调用 [**WheaHwErrorReportSetSeverityDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsetseveritydevicedriver) 来设置数据包和部分的错误严重性。 另请参阅 [**WheaHwErrorReportSetSectionNameDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsetsectionnamedevicedriver)，它是用于更新 [**WHEA_ERROR_RECORD_SECTION_DESCRIPTOR**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor) 结构的 FRUText 字段的 helper 函数。

3. 将错误数据复制到缓冲区集。

4. 再次调用 [**WheaHwErrorReportSubmitDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsubmitdevicedriver)，提供错误句柄。 在此调用之后，缓冲区集中的缓冲区不可用，该句柄无效。

5. 如果发生错误或错误不再有效，则驱动程序可以选择调用 [**WheaHwErrorReportAbandonDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportabandondevicedriver)。 在这种情况下，不会向 WHEA 提交任何报表。

驱动程序必须在 [**WheaCreateHwErrorReportDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheacreatehwerrorreportdevicedriver)创建的每个句柄上调用 [**WheaHwErrorReportSubmitDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportsubmitdevicedriver)或 [**WheaHwErrorReportAbandonDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheahwerrorreportabandondevicedriver) 。 否则， [**WheaRemoveErrorSourceDeviceDriver**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver) 可能返回 STATUS_RESOURCE_IN_USE。
