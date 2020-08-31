---
title: 线程和同步第一级别
description: 线程和同步第一级别
ms.assetid: 9fce6a18-2a66-4518-b05b-e85bdaa3951f
keywords:
- 线程 WDK 显示，第一级
- 同步 WDK 显示，第一级
ms.date: 08/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: f91e14dde99a63fb7a0c5167ab4dba1a528ea5eb
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063768"
---
# <a name="threading-and-synchronization-first-level"></a>线程和同步第一级别

Windows 显示驱动程序模型 (WDDM) 将调用分为显示微型端口驱动程序，该驱动程序是在第一个线程级别下进行的，并同步到以下 nonreentrancy 类。 在特定类中不允许重入;也就是说，只有一个线程可以在特定类中输入驱动程序。 但是，可以同时输入来自多个第一层类和 [零级别](threading-and-synchronization-zero-level.md) 调用的调用。

> [!NOTE]
>
> 尽管 [不同的第](threading-and-synchronization-zero-level.md) 一层类中的两个或多个线程可以同时在驱动程序中运行，但不能有两个线程属于单个进程。

## <a name="pointer-class"></a>指针类

Windows 显示驱动程序模型 (WDDM) 不允许以可重入方式调用某个指针类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

* [*DxgkDdiSetPointerPosition*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)
* [*DxgkDdiSetPointerShape*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)

## <a name="gpu-scheduler-class"></a>GPU 计划程序类

Windows 显示器驱动程序模型 (WDDM) 不允许以可重入方式调用某个 GPU 计划程序加载器类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

* [*DxgkDdiBuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)
* [*DxgkDdiPatch*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)
* [*DxgkDdiPreemptCommand*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)
* [*DxgkDdiQueryDependentEngineGroup*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)
* [*DxgkDdiQueryEngineStatus*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus)
* [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)
* [*DxgkDdiSubmitCommand*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)

## <a name="swizzling-range-class"></a>重排范围类

Windows 显示驱动程序模型 (WDDM) 不允许以可重入方式调用 swizzling 范围类函数之一。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

* [*DxgkDdiAcquireSwizzlingRange*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)
* [*DxgkDdiReleaseSwizzlingRange*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)

## <a name="overlay-class"></a>覆盖类

Windows 显示驱动程序模型 (WDDM) 不允许以可重入方式调用某个覆盖类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

* [*DxgkDdiCreateOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)
* [*DxgkDdiDestroyOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)
* [*DxgkDdiFlipOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)
* [*DxgkDdiUpdateOverlay*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)

## <a name="child-io-class"></a>子 I/O 类

Windows 显示驱动程序模型 (WDDM) 不允许以可重入方式调用子 i/o 类函数之一。 也就是说，在给定的时间，每个子设备的以下功能中最多可以运行一个线程：

> [!NOTE]
>
> 子 i/o 类函数按子设备进行同步 (也就是说，允许同时调用多个子设备) 。 但是，如果子设备之间存在内部依赖关系，则显示微型端口驱动程序必须根据需要阻止调用。

* [*DxgkDdiQueryChildStatus*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)
* [DxgkDdiQueryConnectionChange](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryconnectionchange)
* [*DxgkDdiQueryDeviceDescriptor*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)
* [*DxgkDdiDisplayDetectControl*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_displaydetectcontrol)
* [*DxgkDdiI2CReceiveDataFromDisplay*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_receive_data_from_display)
* [*DxgkDdiI2CTransmitDataToDisplay*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_transmit_data_to_display)
* [*DxgkDdiOPMConfigureProtectedOutput*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)
* [*DxgkDdiOPMCreateProtectedOutput*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)
* [*DxgkDdiOPMDestroyProtectedOutput*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)
* [*DxgkDdiOPMGetCertificate*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)
* [*DxgkDdiOPMGetCertificateSize*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)
* [*DxgkDdiOPMGetCOPPCompatibleInformation*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)
* [*DxgkDdiOPMGetInformation*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)
* [*DxgkDdiOPMGetRandomNumber*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)
* [*DxgkDdiOPMSetSigningKeyAndSequenceNumbers*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)

## <a name="display-class"></a>显示类

Windows 显示驱动程序模型 (WDDM) 不允许以可重入方式调用某个显示类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

* [*DxgkDdiSetTargetGamma*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetgamma)
* [*DxgkDdiSetTargetContentType*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetcontenttype)
* [*DxgkDdiSetTargetAnalogCopyProtection*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetanalogcopyprotection)
* [*DxgkDdiSetTargetAdjustedColorimetry*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry)