---
title: 子 I/O 类
description: 子 I/O 类
ms.assetid: e467ef0c-a969-4cc1-a5b5-2416794051f2
keywords:
- 子 I/O 类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e91ebf81f4592602da288afbfff84fbdd19fc5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525315"
---
# <a name="child-io-class"></a>子 I/O 类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个子调用 I/O 类函数以可重入的方式。 即最，一个线程可以运行在每个子设备的下列函数之一中在给定时间：

-   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_status)

-   [DxgkDdiQueryConnectionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryconnectionchange)

-   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)

-   [*DxgkDdiDisplayDetectControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_displaydetectcontrol)

-   [*DxgkDdiI2CReceiveDataFromDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_i2c_receive_data_from_display)

-   [*DxgkDdiI2CTransmitDataToDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_i2c_transmit_data_to_display)

-   [*DxgkDdiOPMConfigureProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)

-   [*DxgkDdiOPMCreateProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)

-   [*DxgkDdiOPMDestroyProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

-   [*DxgkDdiOPMGetCertificate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)

-   [*DxgkDdiOPMGetCertificateSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)

-   [*DxgkDdiOPMGetCOPPCompatibleInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)

-   [*DxgkDdiOPMGetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)

-   [*DxgkDdiOPMGetRandomNumber*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)

-   [*DxgkDdiOPMSetSigningKeyAndSequenceNumbers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)

 

 





