---
title: 子 I/O 类
description: 子 I/O 类
ms.assetid: e467ef0c-a969-4cc1-a5b5-2416794051f2
keywords:
- 子 i/o 类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f531f6436bbc4bb709740bb57a49c96e63710691
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839810"
---
# <a name="child-io-class"></a>子 I/O 类


Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用子 i/o 类函数之一。 也就是说，在给定的时间，每个子设备的以下功能中最多可以运行一个线程：

-   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)

-   [DxgkDdiQueryConnectionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryconnectionchange)

-   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)

-   [*DxgkDdiDisplayDetectControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_displaydetectcontrol)

-   [*DxgkDdiI2CReceiveDataFromDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_receive_data_from_display)

-   [*DxgkDdiI2CTransmitDataToDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_transmit_data_to_display)

-   [*DxgkDdiOPMConfigureProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)

-   [*DxgkDdiOPMCreateProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)

-   [*DxgkDdiOPMDestroyProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

-   [*DxgkDdiOPMGetCertificate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)

-   [*DxgkDdiOPMGetCertificateSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)

-   [*DxgkDdiOPMGetCOPPCompatibleInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)

-   [*DxgkDdiOPMGetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)

-   [*DxgkDdiOPMGetRandomNumber*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)

-   [*DxgkDdiOPMSetSigningKeyAndSequenceNumbers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)

 

 





