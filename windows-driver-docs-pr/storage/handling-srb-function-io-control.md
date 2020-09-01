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
ms.openlocfilehash: 70fb02e555f324acabafb20135ae6e831b3b8f9c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191301"
---
# <a name="handling-srb_function_io_control"></a>处理 SRB \_ 函数 \_ IO \_ 控件


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


微型端口驱动程序是否处理 \_ SRB \_ 的函数 IO \_ 控制请求取决于 HBA 是否为用户模式应用程序提供专用支持。 如果支持此请求，则允许将一组由驱动程序定义的 ( "专用" ) i/o 控制请求直接发送到微型端口驱动程序。 对于将 **函数** 成员设置为 SRB \_ 函数 \_ IO 控件的 SRBs \_ ， **DataBuffer** 成员包含一个指向系统定义的 SRB IO 控制结构的指针，该 \_ \_ 结构包含驱动程序定义的驱动程序和应用程序指定的 **ControlCode**。

发送到基于 NT 的操作系统存储类驱动程序的所有系统定义的、所需的设备 i/o 控制请求将映射到 SRBs，并将 **函数** 成员设置为 SRB \_ function \_ EXECUTE \_ SCSI，而不是 SRB \_ 函数 \_ IO \_ 控件。

##  <a name="-see--also"></a>-请参阅-还

[处理 SRB_FUNCTION_EXECUTE_SCSI](./handling-srb-function-execute-scsi.md)

[SRB_IO_CONTROL](/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

