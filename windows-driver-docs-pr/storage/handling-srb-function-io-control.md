---
title: 处理 SRB_FUNCTION_IO_CONTROL
description: 处理 SRB_FUNCTION_IO_CONTROL
ms.assetid: 92d09a49-d8e8-4d97-b334-c42d5b04ee8d
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_IO_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcf4211764199d6671ce27fa8f385c7210e74025
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837843"
---
# <a name="handling-srb_function_io_control"></a>处理 SRB\_函数\_IO\_控件


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


微型端口驱动程序是否处理 SRB\_函数\_IO\_控制请求取决于 HBA 是否为用户模式应用程序提供专用支持。 如果支持此请求，则可以将一组驱动程序定义的（"专用"） i/o 控制请求直接发送到微型端口驱动程序。 对于 SRBs 函数成员设置为 SRB\_函数\_IO\_**控件的**， **DataBuffer**成员包含指向系统定义的 SRB 的指针\_io\_控制结构包含驱动程序定义的和应用程序指定的**ControlCode**。

发送到基于 NT 的操作系统存储类驱动程序的所有系统定义的、所需的设备 i/o 控制请求都将映射到 SRBs，并将**函数**成员设置为 SRB\_\_\_函数，而不是 SRB\_函数。\_IO\_控制。

##  <a name="-see--also"></a>-请参阅-还

[处理 SRB_FUNCTION_EXECUTE_SCSI](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-srb-function-execute-scsi)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

 




