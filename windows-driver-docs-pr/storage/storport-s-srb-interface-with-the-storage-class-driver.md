---
title: Storport 的可以与存储类驱动程序交互的 SRB 接口
description: Storport 的可以与存储类驱动程序交互的 SRB 接口
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3884a56c03c423cd0da91762ffeb4021f37b9181
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842833"
---
# <a name="storports-srb-interface-with-the-storage-class-driver"></a>Storport 的可以与存储类驱动程序交互的 SRB 接口


存储类驱动程序和其他较高级别的组件通过构建 SCSI 请求块（SRBs）与 Storport 驱动程序通信。 SRB 包含 SCSI 命令描述符块（CDB）以及一个指向数据缓冲区的指针，该缓冲区用于将数据传输到设备或从设备传输数据（如果有）。 它可能包含一个指向感知缓冲区的指针，该指针用于在 SCSI 命令失败且具有检查条件状态时保存 SCSI 检测数据。 有关 SRBs 的详细信息，请参阅[**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。 存储类驱动程序通过**MajorFunction**成员设置为 IRP\_MJ\_SCSI，将它们创建的 SRBs 传递到 Storport。 有关存储类驱动程序在将 SRB 传递到端口驱动程序之前必须执行的步骤的说明，请参阅[存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

在将 SRB 转发到堆栈之前，Storport 会在 SRB 中设置某些值，例如目标设备的路径、目标号码和逻辑单元号。

与其他端口驱动程序不同，如系统提供的 IDE/ATAPI 端口驱动程序和 IEEE 1394 总线，Storport 无需在将其接收的 SRBs 中转换为其他格式的命令描述符块（CDB），然后将其转发到基础适配器。 Storport 只是向 SRB 添加一些目标特定的信息，并将其传递给具有不改变 CDB 的微端口驱动程序。 因此，Storport 只是将包含 CDBs 的 SRBs 传递到堆栈中。

出于此原因，存储类驱动程序和 Storport 之间的 SRB 接口的大多数方面都涵盖在存储类和存储微型端口驱动程序的一般文档及其随附的参考资料中。 有关存储类驱动程序与 Storport 微型端口驱动程序对之间的 SRB 接口相关的章节列表，请参阅[storport 的使用 Storport 微型端口驱动程序的接口](storport-s-interface-with-storport-miniport-drivers.md)。

 

 




