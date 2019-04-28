---
title: Storport 的可以与存储类驱动程序交互的 SRB 接口
description: Storport 的可以与存储类驱动程序交互的 SRB 接口
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4020cba407f002f60b92aa2b62b0757ffd3dff78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342835"
---
# <a name="storports-srb-interface-with-the-storage-class-driver"></a>Storport 的可以与存储类驱动程序交互的 SRB 接口


存储类驱动程序和其他更高级别的组件与通信 Storport 驱动程序通过构建 SCSI 请求块 (Srb)。 SRB 包含 SCSI 命令描述符块 (CDB) 和是要用来将数据传入或从设备 （如果有） 的数据缓冲区的指针。 它可能包含指向用于事件的 SCSI 命令失败，并检查条件状态中保存 SCSI 检测数据的意义上缓冲区的指针。 有关 Srb 详细信息，请参阅[ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393)。 存储类驱动程序将它们创建 Srb 传递给中与 IRP Storport **MajorFunction**成员设置为 IRP\_MJ\_SCSI。 有关存储类驱动程序必须采取的步骤的说明生成 SRB 然后再将它传递到端口驱动程序，请参阅[存储类驱动程序 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

转发堆栈的下层 SRB 之前, Storport SRB，例如路径、 目标数和目标设备的逻辑单元号中设置某些值。

与其他端口驱动程序，例如 IDE/ATAPI 和 IEEE 1394 总线中，系统提供的端口驱动程序不同 Storport 转换命令描述符块 (CDB) 中没有 Srb 转发到之前接收到不同的格式基础适配器。 Storport 只需添加 SRB 了一些特定于目标的信息并将其原封不动地 cdb 传递给微型端口驱动程序。 因此，Storport 只需将传递在堆栈的下层包含 Cdb Srb。

出于此原因，大多数方面之间的存储类驱动程序和 Storport SRB 接口的文档中介绍了常规的存储类和存储微型端口驱动程序和其随附的参考资料。 到 SRB 接口之间的存储类驱动程序和 Storport 微型端口驱动程序对相关的部分列表，请参阅[Storport 的接口与 Storport 微型端口驱动程序](storport-s-interface-with-storport-miniport-drivers.md)。

 

 




