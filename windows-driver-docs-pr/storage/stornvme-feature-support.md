---
title: StorNVMe 功能支持
description: 介绍 StorNVMe 支持的 NVMe 功能
ms.assetid: 96b62fbb-bcf3-402d-ba29-0a61dc95c92c
ms.date: 08/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 84fd99cf35a6451486601c402e456a5e34d7ca12
ms.sourcegitcommit: 1600bbad585647840839a6f66078c961c337c268
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88203661"
---
# <a name="stornvme-feature-support"></a>StorNVMe 功能支持

下表列出了 NVME 功能，并指出了在 Windows 10 版本1903及更高版本上由 **StorNVMe** 提供的支持。

有关其他信息，请参阅使用 [NVMe 驱动器](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices#protocol-specific-queries) 。

| Feature  | 支持 | 注释 |
| :------- | :-------: | :------- |
| 固件更新过程                                        | X |  支持第1个槽，多个槽用于提交/下载。 与控制器报告的固件更新粒度对齐。 |
| 固件激活而不重置                              | X | |
| 元数据处理                                              |   | |
| 端到端数据保护                                     |   | |
| 电源管理                                               | X | 支持不可操作的电源状态。 默认情况下，将禁用自治电源状态转换。 默认情况下，将为新式备用中的选定平台启用运行时 D3 转换。 主机控制温度管理获取并设置通过 [IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property) 和 [IOCTL_STORAGE_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_property)支持的功能。 |
| 虚拟化增强功能                                    |   | |
| 软件仿真的 Doorbell 步幅                         |   | |
| 标准供应商特定命令格式                        |   | |
| 预留                                                   |   | |
| 主机内存缓冲区                                             | X | |
| 重播受保护的内存块                                  |   | |
| 设备自检操作                                    | X | 无本机支持;通过 [IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)提供的功能。|
| 命名空间管理                                           | X | 无本机支持;在 WinPE 模式下通过 [IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) 提供的功能。 |
| 启动分区                                                |   | |
| 遥测                                                      | X | 通过 [IOCTL_SCSI_PASS_THROUGH](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) 使用带有缓冲模式的命令 SCSIOP_READ_DATA_BUFF16 作为 READ_BUFFER_MODE_ERROR_HISTORY 支持。 还可通过 [IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)通过 StorageAdapterProtocolSpecificProperty/StorageDeviceProtocolSpecificProperty 获得。 对于主机遥测，还可以从 Windows 10 2004 版开始 [IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_device_internal_log) 。 |
| 净化操作                                            | X | 在 WinPE 模式下通过 [IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command) 支持。 |
| 读取恢复级别                                            |   | |
| 耐用性组                                               | X | 可以通过[IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)检索信息 |
| 可预测延迟模式                                       |   | |
| 命名空间写保护                                     |   | |
| 非对称命名空间访问报告                          |   | |
| 获取 LBA 状态                                                 |   | |
| SQ 关联                                                |   | |
| 特定于供应商的信息的 Uuid                          |   | |
| 通过 i/o 大小和一致性来提高性能 | X | 支持命名空间最佳 IO 边界 (NOIOB) 。 当前不支持 NPWG、NPWA、NPDG、NPDA 和 NOWS |

## <a name="reference-links"></a>引用链接

- [使用 NVMe 设备](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices)
- [NVMe 存储协议数据类型](https://docs.microsoft.com/windows/win32/api/winioctl/ne-winioctl-storage_protocol_nvme_data_type)
