---
title: 使用 Storport 进行硬件初始化
description: 使用 Storport 进行硬件初始化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ddc1f047cb2a079d3943c88dae361c72608735
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383107"
---
# <a name="hardware-initialization-with-storport"></a>使用 Storport 进行硬件初始化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport 驱动程序遵循 SCSI 端口驱动程序的插即用 (PnP) 初始化模型。 在驱动程序的过程[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，微型端口驱动程序调用[ **StorPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff567108)例程替换[ **HW\_初始化\_数据 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff557459)结构描述它支持的硬件。 随后，当 PnP 管理器会调用端口驱动程序[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，端口驱动程序调用微型端口驱动程序[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)例程替换[**端口\_配置\_信息 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)结构，然后通过调用微型端口驱动程序的[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)例程，以初始化适配器。

大多数情况下，Storport 版本的 HW\_初始化\_数据结构是由与 SCSI 端口一起使用的相同名称的结构相同。

部分中所示[使用的映射中的缓冲区 Storport I/O 模型](use-of-mapping-buffers-in-the-storport-i-o-model.md)，则**MapBuffers**的这两个硬件成员\_初始化和端口\_配置\_信息在 Storport 情况下，从在 SCSI 端口的情况下具有不同的含义。

 

 




