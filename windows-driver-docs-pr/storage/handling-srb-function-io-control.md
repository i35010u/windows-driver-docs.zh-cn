---
title: 处理 SRB_FUNCTION_IO_CONTROL
description: 处理 SRB_FUNCTION_IO_CONTROL
ms.assetid: 92d09a49-d8e8-4d97-b334-c42d5b04ee8d
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_IO_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1eaf4fbc5bdc9013cc6b0fdc739e01d009976d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325972"
---
# <a name="handling-srbfunctioniocontrol"></a>处理 SRB\_函数\_IO\_控件


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


微型端口驱动程序是否处理 SRB\_函数\_IO\_控件请求取决于 HBA 是为在用户模式应用程序提供专门的支持。 支持此请求允许驱动程序定义 （"私有"） 需的 I/O 控制请求直接发送到微型端口驱动程序集。 有关与 Srb**函数**成员设置为 SRB\_函数\_IO\_控件， **DataBuffer**成员包含一个指向系统定义 SRB\_IO\_包含驱动程序定义和应用程序指定的控件结构**ControlCode**。

发送到基于 NT 的操作系统存储类驱动程序的所有系统定义的所需设备 I/O 控制请求映射到与 Srb**函数**成员设置为 SRB\_函数\_EXECUTE\_SCSI，不适用于 SRB\_函数\_IO\_控件。

##  <a name="-see--also"></a>-see -also

[Handling SRB_FUNCTION_EXECUTE_SCSI](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-srb-function-execute-scsi)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ns-ntddscsi-_srb_io_control)

 




