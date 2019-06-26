---
title: SCSI 端口的可以与存储类驱动程序交互的 SRB 接口
description: SCSI 端口的可以与存储类驱动程序交互的 SRB 接口
ms.assetid: ca30bf9b-6d76-4160-8a4e-54c681dfc843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a46fb4501c966f6cc00ae1e0c68c2b669019fda9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363365"
---
# <a name="scsi-ports-srb-interface-with-the-storage-class-driver"></a>SCSI 端口的可以与存储类驱动程序交互的 SRB 接口


## <span id="ddk_scsi_ports_srb_interface_with_the_storage_class_driver_kg"></span><span id="DDK_SCSI_PORTS_SRB_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序和其他更高级别的组件与通信 SCSI 端口驱动程序通过构建 SCSI 请求块 (Srb)。 有关 Srb 详细信息，请参阅[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)。 存储类驱动程序将它们创建 Srb 传递给 SCSI 端口中使用 IRP **MajorFunction**成员设置为 IRP\_MJ\_SCSI。 有关存储类驱动程序必须采取的步骤的说明生成 SRB 然后再将它传递到端口驱动程序，请参阅[存储类驱动程序 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

转发堆栈的下层 SRB 之前, SCSI 端口 SRB，例如端口号、 路径、 目标数和目标设备的逻辑单元号中设置某些值。

与其他端口驱动程序，例如 IDE/ATAPI 和 IEEE 1394 总线中，系统提供的端口驱动程序不同 SCSI 端口转换命令描述符块 (CDB) 中没有它接收到不同的格式，再转发到 Srb基础适配器。 SCSI 端口只需添加 SRB 了一些特定于目标的信息并将其原封不动地 cdb 传递给微型端口驱动程序。 因此，SCSI 端口是只需将传递在堆栈的下层包含 Cdb Srb messenger。

出于此原因，存储类和存储微型端口驱动程序和其随附的参考资料的常规文档中介绍的存储类驱动程序和 SCSI 端口之间的 SRB 接口的大多数方面。 到 SRB 接口之间的存储类驱动程序和 SCSI 端口微型端口驱动程序对相关的部分列表，请参阅[SCSI 端口 SCSI 端口微型端口驱动程序接口](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)。

 

 




