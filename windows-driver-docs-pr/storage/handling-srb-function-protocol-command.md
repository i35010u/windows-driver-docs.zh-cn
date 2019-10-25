---
title: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
description: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
ms.assetid: 12e9791b-8ddf-4d42-9d89-243bc38eeeb7
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_PROTOCOL_COMMAND
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 72ec9f0ba690b2ea9d9d9e2a1cff0bfaf50d2ebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833735"
---
# <a name="handling-srb_function_protocol_command"></a>处理 SRB_FUNCTION_PROTOCOL_COMMAND

当 HBA 要为用户模式应用程序提供专用支持时，微型端口驱动程序处理 SRB_FUNCTION_PROTOCOL_COMMAND 请求。 如果支持此请求，则允许将一组驱动程序定义的（"专用"）协议命令直接发送到微型端口驱动程序。

对于将**函数**成员设置为 SRB_FUNCTION_PROTOCOL_COMMAND 的 SRBs， **DataBuffer**成员包含指向系统定义的[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command)结构的指针。

微型端口应执行以下操作：

* 将 STORAGE_PROTOCOL_COMMAND 结构中提供的命令信息转换为相应的特定于协议的总线命令。 协议由 **\*数据 > ProtocolType**标识。

* 对于写入类型请求，将**DataToDeviceBufferOffset**指向设备的数据传输到。

* 对于读取类型请求，请将数据从设备传输到**DataFromDeviceBufferOffset**指向的缓冲区。

* 设置**ReturnStatus**以反映请求的状态，并选择性地设置**错误代码**。

## <a name="see-also"></a>另请参阅

[IOCTL_STORAGE_PROTOCOL_COMMAND （*winioctl*）](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-ioctl_storage_protocol_command)

[IOCTL_STORAGE_PROTOCOL_COMMAND （*ntddstor*）](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)

[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

[SCSI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)

[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command)

[STORAGE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_storage_request_block)
