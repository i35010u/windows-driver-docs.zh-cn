---
title: 使 SCSI 端口微型端口驱动程序适用于 Storport
description: 使 SCSI 端口微型端口驱动程序适用于 Storport
ms.assetid: d2e8daaf-47e2-4a6c-9992-517dc107d4bd
keywords:
- Storport 驱动程序 WDK，SCSI 端口微型端口驱动程序
- SCSI 端口驱动程序 WDK 存储、 Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09711e8b3ca0bba7c2b2c40db8b1042b5c0e5977
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355575"
---
# <a name="making-scsi-port-miniport-drivers-work-with-storport"></a>使 SCSI 端口微型端口驱动程序适用于 Storport


## <span id="ddk_making_scsi_port_miniport_drivers_work_with_storport_kg"></span><span id="DDK_MAKING_SCSI_PORT_MINIPORT_DRIVERS_WORK_WITH_STORPORT_KG"></span>


Storport 微型端口驱动程序接口旨在为类似于 SCSI 端口微型端口驱动程序接口尽可能情况下，为了简化修改的 SCSI 端口微型端口驱动程序才能正常使用 Storport 驱动程序。 为了使使用 Storport SCSI 端口微型端口驱动程序，必须执行以下基本步骤：

1.  所有实例都更改 **\#包括** &lt; *scsi.h* &gt;指令与 **\#包括** &lt; *storport.h* &gt;指令。

    如果这两个*scsi.h*并*storport.h*标头将包含的文件，将发生编译时错误。

2.  替换为 s*csiport.lib*与*storport.lib*生成脚本，也就是说，在源中或**生成文件**文件。

3.  请确保已正确初始化扩展的所有结构。

    这两者的大小[ **HW\_初始化\_数据 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456)结构和[**端口\_配置\_信息 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff563900)结构已更改，因此请确保已正确初始化的新成员。

Storport 标头文件， *storport.h，* 目前所保持的 SCSI 端口作为前缀的命令和 StorPort 前缀命令以便从 SCSI 端口移植。

本部分提供有关驱动程序编写人员想要修改用于处理与 SCSI 端口，以便它可以使用 Storport 微型端口驱动程序的更多详细的说明。 论述了以下主题：

[Storport 使用了适配器的要求](requirements-for-using-storport-with-an-adapter.md)

[使用 Storport 硬件初始化](hardware-initialization-with-storport.md)

[Storport 设置端口配置信息](setting-port-configuration-information-with-storport.md)

 

 




