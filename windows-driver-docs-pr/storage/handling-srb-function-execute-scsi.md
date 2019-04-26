---
title: 处理 SRB_FUNCTION_EXECUTE_SCSI
description: 处理 SRB_FUNCTION_EXECUTE_SCSI
ms.assetid: 221e1070-12d8-4870-a23c-426ed4a25b84
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_EXECUTE_SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87da85d7f9a496f29d86c7ef2b34ba25f06f276e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325987"
---
# <a name="handling-srbfunctionexecutescsi"></a>处理 SRB\_函数\_EXECUTE\_SCSI


## <span id="ddk_handling_srb_function_execute_scsi_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_EXECUTE_SCSI_KG"></span>


大部分 Srb 更高级别的存储类驱动程序已加载后，发送到[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)例程具有**函数**成员设置为 SRB\_函数\_EXECUTE\_SCSI。

在收到 SRB\_函数\_EXECUTE\_SCSI 请求、 微型端口驱动程序*HwScsiStartIo*例程执行以下操作：

-   获取和/或设置微型端口驱动程序保持在其设备、 逻辑单元和/或 SRB 扩展任何上下文

    例如，微型端口驱动程序可能会设置具有指向 SRB 本身和 SRB 的逻辑单元扩展**DataBuffer**指针，SRB **DataTransferLength**值和驱动程序定义值 （或 CDBSCSIOP\_*XXX*值)，该值指示要 HBA 上执行的操作。

-   调用内部例程进行编程的 HBA，作为通过部分定向**SrbFlags**，请求的操作

    对于设备 I/O 操作，此类的内部例程通常选择目标设备，并将 CDB 通过总线发送到目标逻辑单元。

如果微型端口驱动程序使用系统 DMA，它必须调用[ **ScsiPortIoMapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff564649)*之前*编程 HBA 将数据传输。 **ScsiPortIoMapTransfer**将设置系统 DMA 控制器，调用微型端口驱动程序*HwScsiDmaStarted*日常的更高版本中所述[SCSI 微型端口驱动程序 HwScsiDmaStarted 例程](scsi-miniport-driver-s-hwscsidmastarted-routine.md).

发送到基于 NT 的操作系统存储类驱动程序的所有系统定义的所需设备 I/O 控制请求映射到与 Srb**函数**成员设置为 SRB\_函数\_EXECUTE\_SCSI。

 

 




