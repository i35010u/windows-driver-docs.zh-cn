---
title: Storport 的可以与存储类驱动程序交互的 SRB 接口
description: Storport 的可以与存储类驱动程序交互的 SRB 接口
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 326a35a66f8120c0b6f01810c0545149cea4865a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189035"
---
# <a name="storports-srb-interface-with-the-storage-class-driver"></a>Storport 的可以与存储类驱动程序交互的 SRB 接口


存储类驱动程序和其他较高级别的组件通过构建 SCSI 请求块 (SRBs) 与 Storport 驱动程序通信。 SRB 包含 SCSI 命令描述符块 (CDB) ，以及一个指向数据缓冲区的指针，该数据缓冲区用于在任何) 时将数据传入或传出设备 (。 它可能包含一个指向感知缓冲区的指针，该指针用于在 SCSI 命令失败且具有检查条件状态时保存 SCSI 检测数据。 有关 SRBs 的详细信息，请参阅 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。 存储类驱动程序通过将 MajorFunction 成员设置为 IRP MJ SCSI，将它们创建的 SRBs 传递到**MajorFunction**成员 \_ \_ 。 有关存储类驱动程序在将 SRB 传递到端口驱动程序之前必须执行的步骤的说明，请参阅 [存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

在将 SRB 转发到堆栈之前，Storport 会在 SRB 中设置某些值，例如目标设备的路径、目标号码和逻辑单元号。

与其他端口驱动程序不同，如系统提供的用于 IDE/ATAPI 和 IEEE 1394 总线的端口驱动程序，在将命令描述符块接收到不同的格式之前，不需要将其接收到的 SRBs 中的命令描述符)  (块转换为不同的格式，然后将其转发到基础适配器。 Storport 只是向 SRB 添加一些目标特定的信息，并将其传递给具有不改变 CDB 的微端口驱动程序。 因此，Storport 只是将包含 CDBs 的 SRBs 传递到堆栈中。

出于此原因，存储类驱动程序和 Storport 之间的 SRB 接口的大多数方面都涵盖在存储类和存储微型端口驱动程序的一般文档及其随附的参考资料中。 有关存储类驱动程序与 Storport 微型端口驱动程序对之间的 SRB 接口相关的章节列表，请参阅 [storport 的使用 Storport 微型端口驱动程序的接口](storport-s-interface-with-storport-miniport-drivers.md)。

 

