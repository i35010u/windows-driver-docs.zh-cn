---
title: StorNVMe 命令集支持
description: 介绍 StoreNVMe 提供的命令集支持
ms.date: 08/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5dabded70052f05b9c6ad4a0ba88014582251097
ms.sourcegitcommit: 322c5442dc72980ca3a45ad758c70acdf44dc6c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2021
ms.locfileid: "105616679"
---
# <a name="stornvme-command-set-support"></a>StorNVMe 命令集支持

下表列出了 NVMe *Admin* 和 *NVM* 命令集及关联的操作码，并指明了 Windows 10 版本1903及更高版本上的 **StorNVMe** 提供的支持。  

有关其他信息，请参阅使用 [NVMe 驱动器](/windows/win32/fileio/working-with-nvme-devices#protocol-specific-queries) 。

## <a name="admin-command-set-support"></a>管理命令集支持

| 操作码  | NVMe 命令                | StorNVMe 支持      | 注释 |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | 删除 i/o 提交队列 | 内部驱动程序使用情况 |    |
| 1       | 创建 i/o 提交队列 | 内部驱动程序使用情况 |    |
| 2       | 获取日志页                | 内部驱动程序使用情况; [IOCTL_STORAGE_QUERY_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property) |   |
| 4       | 删除 i/o 完成队列 | 内部驱动程序使用情况 |   |
| 5       | 创建 i/o 完成队列 | 内部驱动程序使用情况 |
| 6       | 识别                    | 内部驱动程序使用情况; [IOCTL_STORAGE_QUERY_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)，IOCTL_STORAGE_FIRMWARE_GET_INFO |   |
| 8       | 中止                       |   | 目前不受支持。 |
| 9       | 设置功能                | 内部驱动程序使用情况; [IOCTL_STORAGE_SET_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_property) | 仅对主机控制的热量管理设置了[IOCTL_STORAGE_SET_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_property)的功能 |
| 啊      | 获取功能                | 内部驱动程序使用情况; [IOCTL_STORAGE_QUERY_PROPERTY](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property) |   |
| 48      | 异步事件请求  | 内部驱动程序使用情况 |   |   |
| Dh      | 命名空间管理        | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 10h     | 固件提交             | [IOCTL_STORAGE_FIRMWARE_ACTIVATE](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_activate) | |
| 11h     | 固件映像下载     | [IOCTL_STORAGE_FIRMWARE_DOWNLOAD](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_download) | |
| 14h     | 设备 Self-Test            | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)  | |
| 15h     | 命名空间附件        | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 19h     | 指令发送              | 内部驱动程序使用情况 |   |
| 1Ah     | 指令接收           | 内部驱动程序使用情况 |   |
| 1Ch     | 虚拟化管理   |   | 目前不受支持。 |
| 1Dh     | NVMe-英里发送                | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 1Eh     | NVMe-英里接收             | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 7Ch     | Doorbell Buffer Config      |   | 目前不受支持。 |
| 80h     | 格式 NVM                  | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)、 [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)、 [IOCTL_STORAGE_REINITIALIZE_MEDIA](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reinitialize_media) | 仅在 Win PE 模式下为 [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用。 [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_SANITIZE。 IOCTL_STORAGE_REINITIALIZE_MEDIA 仅支持加密擦除。 |
| 81h     | 安全发送               | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_SECURITY_PROTOCOL_OUT |
| 82h     | 安全接收            | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_SECURITY_PROTOCOL_IN |
| 84h     | 净化                    | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 86h     | 获取 LBA 状态              |   | 目前不受支持。 |
| C0h-FFh | 特定于供应商             | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 特定于供应商的传递命令。 要求控制器支持命令效果日志，并且供应商命令的命令效果数据应报告为受支持。 |

## <a name="nvm-command-set-support"></a>NVM 命令集支持

| 操作码  | NVMe 命令                | StorNVMe 支持      | 注释 |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | 刷新                       | 内部驱动程序使用情况， [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_SYNCHRONIZE_CACHE |
| 1       | 写入                       | 内部驱动程序使用情况， [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_WRITE/SCSIOP_WRITE16 |
| 2       | 读取                        | 内部驱动程序使用情况， [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_READ/SCSIOP_READ16 |
| 4       | 写入无法纠正         |   | 目前不受支持。 |
| 5       | 比较                     | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 仅在 Win PE 模式下为[IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)启用 |
| 8       | 写零                |   | 目前不受支持。 |
| 9       | 数据集管理          | [IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) | 仅剪裁 (释放) ;[IOCTL_SCSI_PASS_THROUGH](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)的 SCSIOP_UNMAP |
| 48      | 验证                      |   | 目前不受支持。 |
| Dh      | 预订注册        |   | 目前不受支持。 |
| 吧      | 预订报表          |   | 目前不受支持。 |
| 11h     | 预留获取         |   | 目前不受支持。 |
| 15h     | 保留发布         |   | 目前不受支持。 |
| 80h-FFh | 特定于供应商             | [IOCTL_STORAGE_PROTOCOL_COMMAND](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) | 特定于供应商的传递命令。 要求控制器支持命令效果日志，并且供应商命令的命令效果数据应报告为受支持。 |
