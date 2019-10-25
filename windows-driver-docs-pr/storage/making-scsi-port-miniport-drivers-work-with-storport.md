---
title: 使 SCSI 端口微型端口驱动程序适用于 Storport
description: 使 SCSI 端口微型端口驱动程序适用于 Storport
ms.assetid: d2e8daaf-47e2-4a6c-9992-517dc107d4bd
keywords:
- Storport 驱动程序 WDK，SCSI 端口微型端口驱动程序
- SCSI 端口驱动程序 WDK 存储、Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 910144a89d5d26a59cf0fa0e97eaa2cd2f75671b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841614"
---
# <a name="making-scsi-port-miniport-drivers-work-with-storport"></a>使 SCSI 端口微型端口驱动程序适用于 Storport


## <span id="ddk_making_scsi_port_miniport_drivers_work_with_storport_kg"></span><span id="DDK_MAKING_SCSI_PORT_MINIPORT_DRIVERS_WORK_WITH_STORPORT_KG"></span>


Storport-微型端口驱动程序接口设计为尽可能类似于 SCSI 端口-微型端口驱动程序接口，以便更好地适应使用 Storport 驱动程序的 SCSI 端口微型端口驱动程序。 若要使 SCSI 端口微型端口驱动程序可与 Storport 一起使用，必须执行以下基本步骤：

1.  更改\#的所有实例**包括**&lt;的*scsi-3*&gt; 指令， **\#包括**&lt;*storport*&gt; 指令。

    如果同时包含了*scsi-3*和*storport*标头文件，则会发生编译时错误。

2.  在生成脚本中将*csiport*替换为*storport .lib* ，即源或**生成**文件文件中的。

3.  请确保已正确初始化所有扩展的结构。

    [**HW\_初始化\_数据（scsi）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)结构和[**端口\_配置\_信息（scsi）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构的大小已更改，因此请确保新成员已正确初始化。

Storport 标头文件*storport*目前保留 scsi 端口前缀前缀命令和 Storport 前缀的命令，以便于从 SCSI 端口进行移植。

本部分提供了有关驱动程序编写器的更多详细说明，这些编写器希望修改专用于 SCSI 端口的微型端口驱动程序，使其可以与 Storport 一起工作。 论述了以下主题：

[对适配器使用 Storport 的要求](requirements-for-using-storport-with-an-adapter.md)

[用 Storport 进行硬件初始化](hardware-initialization-with-storport.md)

[用 Storport 设置端口配置信息](setting-port-configuration-information-with-storport.md)

 

 




