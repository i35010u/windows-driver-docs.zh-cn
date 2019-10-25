---
title: 使用 Storport 进行硬件初始化
description: 使用 Storport 进行硬件初始化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97dfe054da0a59d71589effdb39fd323027bc681
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838002"
---
# <a name="hardware-initialization-with-storport"></a>使用 Storport 进行硬件初始化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport 驱动程序遵循 SCSI 端口驱动程序的即插即用（PnP）初始化模型。 在驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程期间，微型端口驱动程序使用[**HW\_初始化\_数据（STORPORT）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)结构调用[**StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程，该结构描述了它支持的硬件。 稍后，当 PnP 管理器调用端口驱动程序的[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程时，端口驱动程序使用端口调用微型端口驱动程序的[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)例程， [ **\_配置\_信息（STORPORT）** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构，后跟通过调用微型端口驱动程序的[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)例程来初始化适配器。

大多数情况下，\_数据结构的 Storport 版本的 HW\_初始化与用于 SCSI 端口的相同名称的结构相同。

如在[storport I/o 模型中使用映射缓冲区](use-of-mapping-buffers-in-the-storport-i-o-model.md)中所述，\_初始化和端口\_配置\_信息在 storport 事例**中的含义**不同于这种情况。

 

 




