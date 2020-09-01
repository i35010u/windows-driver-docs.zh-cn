---
title: SCSI 端口的可以与存储类驱动程序交互的 SRB 接口
description: SCSI 端口的可以与存储类驱动程序交互的 SRB 接口
ms.assetid: ca30bf9b-6d76-4160-8a4e-54c681dfc843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a0182ec1492dece8c911e6cb5caa31ecce1761
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187775"
---
# <a name="scsi-ports-srb-interface-with-the-storage-class-driver"></a>SCSI 端口的可以与存储类驱动程序交互的 SRB 接口


## <span id="ddk_scsi_ports_srb_interface_with_the_storage_class_driver_kg"></span><span id="DDK_SCSI_PORTS_SRB_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序和其他更高级组件通过构建 SCSI 请求块 (SRBs) 来与 SCSI 端口驱动程序通信。 有关 SRBs 的详细信息，请参阅 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。 存储类驱动程序将其创建的 SRBs 传递到 IRP，并将 **MajorFunction** 成员设置为 irp \_ MJ \_ SCSI。 有关存储类驱动程序在将 SRB 传递到端口驱动程序之前必须执行的步骤的说明，请参阅 [存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

在堆栈中转发 SRB 之前，SCSI 端口会在 SRB 中设置某些值，例如端口号、路径、目标号码和目标设备的逻辑单元号。

不同于其他端口驱动程序，如 IDE/ATAPI 和 IEEE 1394 总线的系统提供的端口驱动程序，SCSI 端口无需将命令描述符 (块转换为 SRBs 中的 CDB) ，然后将其接收到其他格式，然后将其转发到基础适配器。 SCSI 端口只是将一些特定于目标的信息添加到 SRB，并将其传递到具有更改的 CDB 的微型端口驱动程序。 因此，SCSI 端口只是传递包含 CDBs 的 SRBs 的信使。

出于此原因，存储类驱动程序和 SCSI 端口之间的 SRB 接口的大多数方面都涵盖在存储类和存储微型端口驱动程序的一般文档及其随附的参考资料中。 有关存储类驱动程序与 SCSI 端口-微型端口驱动程序对之间的 SRB 接口相关的章节列表，请参阅 [使用 scsi 端口微型端口驱动程序的 Scsi 端口接口](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)。

 

