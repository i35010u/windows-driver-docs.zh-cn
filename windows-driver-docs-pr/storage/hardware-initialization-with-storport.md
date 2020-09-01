---
title: 使用 Storport 进行硬件初始化
description: 使用 Storport 进行硬件初始化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9babcda6e54e894a0686d479c045ccb2c9ffbb31
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186693"
---
# <a name="hardware-initialization-with-storport"></a>使用 Storport 进行硬件初始化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport 驱动程序遵循 SCSI 端口驱动程序的即插即用 (PnP) 初始化模型。 在驱动程序的[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程期间，微型端口驱动程序将使用[**HW \_ 初始化数据（ \_ (STORPORT) **](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)结构）调用[**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程，该数据描述它支持的硬件。 稍后，当 PnP 管理器调用端口驱动程序的 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程时，端口驱动程序将使用端口配置信息调用微型端口驱动程序的 [**HWSTORFINDADAPTER**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) 例程 [** \_ \_ (STORPORT) **](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)) 结构，然后调用微型端口驱动程序的 [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) 例程来初始化适配器。

大多数情况下，HW 初始化数据结构的 Storport 版本 \_ 与 \_ 用于 SCSI 端口的相同名称的结构相同。

如在[storport I/o 模型中使用映射缓冲区](use-of-mapping-buffers-in-the-storport-i-o-model.md)中所述，在此情况下， **MapBuffers**硬件 \_ 初始化和端口配置信息的 MapBuffers 成员在 \_ \_ storport 情况下具有不同的含义。

 

