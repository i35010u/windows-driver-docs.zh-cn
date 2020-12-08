---
title: 将 Storport 与适配器配合使用的要求
description: 将 Storport 与适配器配合使用的要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8efe59851bc2cf00985cd9fc1ebe87a24744d48d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801247"
---
# <a name="requirements-for-using-storport-with-an-adapter"></a>将 Storport 与适配器配合使用的要求


## <span id="ddk_requirements_for_using_storport_with_an_adapter_kg"></span><span id="DDK_REQUIREMENTS_FOR_USING_STORPORT_WITH_AN_ADAPTER_KG"></span>


为提高性能并提高稳定性，Storport 不支持对某些设备提供支持 (主要是) 有限功能集的旧设备。 除了性能下降之外，对这些设备的支持会使端口驱动程序复杂化，同时降低微型端口驱动程序的开发和测试速度。

以下列表详细说明了设备、适配器和微型端口驱动程序必须支持的功能，以便与 Storport 一起工作：

-   总线控制 DMA。 Storport 不支持程控 i/o 或从属模式 DMA。

-   散点/集合 i/o。 微型端口驱动程序必须在其散播/聚集列表实现中至少支持16个物理中断。 与 Storport 一起使用的微型端口驱动程序应能够以与 SCSI 端口微型端口驱动程序相同的方式支持多达255的物理中断。

-   SCSI 标记的队列。 Storport 驱动程序将每个逻辑单元发出多达254请求。 使用 scsi 端口从不发出每个适配器超过254请求的事实的 SCSI 端口微型驱动程序必须进行修改，以接受更多数量的请求。

-   SCSI autorequest 的意义。 不支持禁用。

-   支持较大的感知缓冲区。 在视图中，不能使用固定大小的感知缓冲区设计适用于 Storport 的微型端口驱动程序。 微型端口驱动程序必须使用 SRB 中传递的大小。

-   即插即用。 由于必须为即插即用启用使用 Storport 的微型端口驱动程序，因此端口驱动程序会负责所有共享资源的获取和管理。

-   多层重置。 适配器必须支持分层重置。 有关详细信息，请参阅 [Storport 中的多层重置](multi-tier-reset-in-storport.md)。

-   为了支持 SCSI 查询重要的产品数据页面00h、80h 和83h 版，需要公开虚拟逻辑单元的 RAID 适配器。 例如，对于以下页面，基于主机的 RAID 适配器必须对 "重要产品数据" 页设置为01h 的 SCSI 查询命令进行响应： 0 (支持的重要产品数据页) 、80h (unit 序列号页) 和83h 页 (设备标识页) 。 这些命令可以通过适配器的固件来处理，也可以合成在微型端口驱动程序中。

 

 




