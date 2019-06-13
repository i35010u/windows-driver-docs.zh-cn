---
title: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
description: 处理 SRB_FUNCTION_PROTOCOL_COMMAND
ms.assetid: 12e9791b-8ddf-4d42-9d89-243bc38eeeb7
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_PROTOCOL_COMMAND
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 28edfc66ec1b1f1be90b90fd34052b25c79c6377
ms.sourcegitcommit: d2e67f2be9611c583b8b6589b38fe371585b68f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67037988"
---
# <a name="handling-srbfunctionprotocolcommand"></a>处理 SRB_FUNCTION_PROTOCOL_COMMAND

微型端口驱动程序处理 SRB_FUNCTION_PROTOCOL_COMMAND 请求时 HBA 是为在用户模式应用程序提供专门的支持。 支持此请求允许一组的驱动程序定义 （"私有"） 的协议命令发送直接到微型端口驱动程序。

有关与 Srb**函数**成员设置为 SRB_FUNCTION_PROTOCOL_COMMAND， **DataBuffer**成员包含系统定义的指针[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_protocol_command)结构。

微型端口应执行以下操作：

* 转换到适当的特定于协议的总线命令提供 STORAGE_PROTOCOL_COMMAND 结构中的命令信息。 协议由 **\*数据-> Buffer.ProtocolType**。

* 对于写入类型的请求，将数据传输到该**DataToDeviceBufferOffset**指向该设备。

* 对于读取类型的请求，将数据传输从设备到缓冲区的**DataFromDeviceBufferOffset**指向。

* 设置**ReturnStatus**来反映请求的状态，并 （可选） 设置**ErrorCode**。

## <a name="see-also"></a>请参阅

[IOCTL_STORAGE_PROTOCOL_COMMAND (*winioctl.h*)](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-ioctl_storage_protocol_command)

[IOCTL_STORAGE_PROTOCOL_COMMAND (*ntddstor.h*)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)

[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ns-ntddscsi-_srb_io_control)

[SCSI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)

[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_protocol_command)

[STORAGE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_storage_request_block)
