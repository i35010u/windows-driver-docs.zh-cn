---
title: 将 Storport 与适配器配合使用的要求
description: 将 Storport 与适配器配合使用的要求
ms.assetid: 85adf2f9-e9eb-40d8-9177-adda150a8ea4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 845db304e2823be4be07648d809f302ec1a29404
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352623"
---
# <a name="requirements-for-using-storport-with-an-adapter"></a>将 Storport 与适配器配合使用的要求


## <span id="ddk_requirements_for_using_storport_with_an_adapter_kg"></span><span id="DDK_REQUIREMENTS_FOR_USING_STORPORT_WITH_AN_ADAPTER_KG"></span>


为了提高性能和增强的稳定性，Storport 不提供某些类型的设备 （主要是较旧设备具有有限的功能集） 的支持。 除了会降低性能，对这些设备会增加复杂性端口驱动程序，减的前提下微型端口驱动程序开发和测试的支持。

以下列表详细说明了支持的功能的设备、 适配器和微型端口驱动程序必须全部，才能正常使用 Storport:

-   总线主控 DMA。 Storport 不支持通过编程方式设置的 I/O 或从属模式 DMA。

-   散播-聚集 I/O。 微型端口驱动程序必须支持至少 16 个物理分隔线，在其散播-聚集列表实现中。 可使用 Storport 微型端口驱动程序应该能够支持最多 255 个物理分隔线 SCSI 端口微型端口驱动程序的方式相同。

-   SCSI 有标记的队列。 Storport 驱动程序将发出到 254 请求每个逻辑单位。 SCSI 端口微型端口驱动程序，请使用这一事实 SCSI 端口永远不会发出每个适配器多于 254 个请求必须进行修改以接受更多的请求。

-   SCSI autorequest 检测。 不支持禁用。

-   对更大的意义上缓冲区的支持。 可使用 Storport 微型端口驱动程序必须未设计为具有固定大小意义上缓冲区视图中。 微型端口驱动程序必须使用 SRB 中传递的大小。

-   Plug and Play。 由于使用 Storport 微型端口驱动程序必须启用 Plug and play，端口驱动程序将负责所有共享的资源获取和管理。

-   多层重置。 适配器必须支持分层重置。 有关详细信息，请参阅[多层重置在 Storport](multi-tier-reset-in-storport.md)。

-   RAID 适配器公开虚拟逻辑单元都需要支持 SCSI 查询的重要产品数据页面 00 h、 80 h 和 83 h。 例如，基于主机的 RAID 适配器必须响应 SCSI 查询命令，同时将设置为该版本的以下页面为重要产品数据页：0 （受支持的重要产品数据页）、 80 h （单元序列号页） 和 83 h （设备标识页）。 这些命令可以处理通过适配器的固件或合成微型端口驱动程序中。

 

 




