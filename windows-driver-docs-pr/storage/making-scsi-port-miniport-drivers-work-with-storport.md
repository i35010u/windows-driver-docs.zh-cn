---
title: 使 SCSI 端口微型端口驱动程序适用于 Storport
description: 使 SCSI 端口微型端口驱动程序适用于 Storport
ms.assetid: d2e8daaf-47e2-4a6c-9992-517dc107d4bd
keywords:
- Storport 驱动程序 WDK，SCSI 端口微型端口驱动程序
- SCSI 端口驱动程序 WDK 存储、Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a401c25a630c0807a8417e38b4934e16082d43
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185109"
---
# <a name="making-scsi-port-miniport-drivers-work-with-storport"></a>使 SCSI 端口微型端口驱动程序适用于 Storport


## <span id="ddk_making_scsi_port_miniport_drivers_work_with_storport_kg"></span><span id="DDK_MAKING_SCSI_PORT_MINIPORT_DRIVERS_WORK_WITH_STORPORT_KG"></span>


Storport-微型端口驱动程序接口设计为尽可能类似于 SCSI 端口-微型端口驱动程序接口，以便更好地适应使用 Storport 驱动程序的 SCSI 端口微型端口驱动程序。 若要使 SCSI 端口微型端口驱动程序可与 Storport 一起使用，必须执行以下基本步骤：

1.  ** \# ** &lt; *scsi.h* &gt; 用** \# include** &lt; *storport* &gt; 指令更改包含 scsi-3 指令的所有实例。

    如果同时包含了 *scsi-3* 和 *storport* 标头文件，则会发生编译时错误。

2.  在生成脚本中将*csiport* 替换为 *storport .lib* ，即源或 **生成** 文件文件中的。

3.  请确保已正确初始化所有扩展的结构。

    [**硬件 \_ 初始化 \_ 数据 (scsi) **](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)结构和[**端口 \_ 配置 \_ 信息 (scsi) **](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构的大小已更改，因此请确保已正确初始化新成员。

Storport 标头文件 *storport* 目前保留 scsi 端口前缀前缀命令和 Storport 前缀的命令，以便于从 SCSI 端口进行移植。

本部分提供了有关驱动程序编写器的更多详细说明，这些编写器希望修改专用于 SCSI 端口的微型端口驱动程序，使其可以与 Storport 一起工作。 论述了以下主题：

[将 Storport 与适配器配合使用的要求](requirements-for-using-storport-with-an-adapter.md)

[使用 Storport 进行硬件初始化](hardware-initialization-with-storport.md)

[使用 Storport 设置端口配置信息](setting-port-configuration-information-with-storport.md)

 

