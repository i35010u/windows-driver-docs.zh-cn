---
title: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
description: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_PROTOCOL_COMMAND
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0d4a1f40043534368c2ff55da2a887d313101768
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804517"
---
# <a name="handling-srb_function_protocol_command"></a>处理 SRB_FUNCTION_PROTOCOL_COMMAND

当 HBA 要为用户模式应用程序提供专用支持时，微型端口驱动程序处理 SRB_FUNCTION_PROTOCOL_COMMAND 请求。 如果支持此请求，则允许将一组驱动程序定义 ( "private" ) 协议命令直接发送到微型端口驱动程序。

对于 SRBs **函数** 成员设置为 SRB_FUNCTION_PROTOCOL_COMMAND 的， **DataBuffer** 成员包含指向系统定义的 [STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command) 结构的指针。

微型端口应执行以下操作：

* 将 STORAGE_PROTOCOL_COMMAND 结构中提供的命令信息转换为相应的特定于协议的总线命令。 协议由 **\* Data >ProtocolType** 标识。

* 对于写入类型请求，将 **DataToDeviceBufferOffset** 指向设备的数据传输到。

* 对于读取类型请求，请将数据从设备传输到 **DataFromDeviceBufferOffset** 指向的缓冲区。

* 设置 **ReturnStatus** 以反映请求的状态，并选择性地设置 **错误代码**。

## <a name="see-also"></a>另请参阅

[IOCTL_STORAGE_PROTOCOL_COMMAND (*winioctl*)](/windows/win32/api/winioctl/ni-winioctl-ioctl_storage_protocol_command)

[IOCTL_STORAGE_PROTOCOL_COMMAND (*ntddstor*)](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)

[HwStorStartIo](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)

[SRB_IO_CONTROL](/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

[SCSI_REQUEST_BLOCK](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)

[STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command)

[STORAGE_REQUEST_BLOCK](/windows-hardware/drivers/ddi/srb/ns-srb-_storage_request_block)
