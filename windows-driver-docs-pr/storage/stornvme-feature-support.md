---
title: StorNVMe 支持的 NVMe 功能
description: StorNVMe 支持的 NVMe 功能
ms.assetid: 96b62fbb-bcf3-402d-ba29-0a61dc95c92c
ms.date: 01/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 15374cbab57e3b87abfb933f165ab50ab88a979e
ms.sourcegitcommit: bc6ee54ecf053edf144aab7eeb811e0d233296d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2020
ms.locfileid: "80435021"
---
# <a name="nvme-features-supported-by-stornvme"></a>StorNVMe 支持的 NVMe 功能

下表列出了 NVME 功能，并指出了在 Windows 10 版本1903及更高版本上由**StorNVMe**提供的支持。

| 功能  | 支持 | Comments |
| :------- | :-------: | :------- |
| 固件更新过程                                        | X |  支持第1个槽，多个槽用于提交/下载。 与控制器报告的固件更新粒度对齐。 |
| 固件激活而不重置                              | X | |
| 元数据处理                                              |   | |
| 端到端数据保护                                     |   | |
| 电源管理                                               | X | 支持不可操作的电源状态。 默认情况下，将禁用自治电源状态转换。 默认情况下，将为新式备用中的选定平台启用运行时 D3 转换。 主机控制温度管理获取并设置通过 IOCTL_STORAGE_QUERY_PROPERTY 和 IOCTL_STORAGE_SET_PROPERTY 支持的功能。 |
| 虚拟化增强功能                                    |   | |
| 软件仿真的 Doorbell 步幅                         |   | |
| 标准供应商特定命令格式                        |   | |
| 预留                                                   |   | |
| 主机内存缓冲区                                             | X | |
| 重播受保护的内存块                                  |   | |
| 设备自检操作                                    | X | 无本机支持;通过 IOCTL_STORAGE_PROTOCOL_COMMAND 提供的功能。|
| 命名空间管理                                           | X | 无本机支持;在 WinPE 模式下通过 IOCTL_STORAGE_PROTOCOL_COMMAND 提供的功能。 |
| 启动分区                                                |   | |
| 遥测                                                      | X | 通过 IOCTL_SCSI_PASS_THROUGH 使用带有缓冲模式的命令 SCSIOP_READ_DATA_BUFF16 作为 READ_BUFFER_MODE_ERROR_HISTORY 支持。 还可通过 IOCTL_STORAGE_QUERY_PROPERTY 通过 StorageAdapterProtocolSpecificProperty/StorageDeviceProtocolSpecificProperty 获得。 对于主机遥测，还可以通过 IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG 获取此功能。 |
| 净化操作                                            | X | 在 WinPE 模式下通过 IOCTL_STORAGE_PROTOCOL_COMMAND 支持。 |
| 读取恢复级别                                            |   | |
| 耐用性组                                               | X | 可以通过 IOCTL_STORAGE_QUERY_PROPERTY 检索信息 |
| 可预测延迟模式                                       |   | |
| 命名空间写保护                                     |   | |
| 非对称命名空间访问报告                          |   | |
| 获取 LBA 状态                                                 |   | |
| SQ 关联                                                |   | |
| 特定于供应商的信息的 Uuid                          |   | |
| 通过 i/o 大小和一致性来提高性能 | X | 支持命名空间最佳 IO 边界（NOIOB）。 当前不支持 NPWG、NPWA、NPDG、NPDA 和 NOWS |

<!---  Everything commented out was provided by Vishal but is not in NVME Spec Section 8

| Directives                                                     | X | Supports Stream and Identify directive |
|                                                                |   | |
| Version Compliance                                             | X | Compliance of version <= 1.4 |
| Recommended Arbitration Burst                                  | X | User could set any value apart from controller reported value through registry key ArbitrationBurst |
| Controller Multi-path IO                                       |   | |
| Namespace sharing capabilities                                 |   | |
| Maximum Data Transfer Size Support                             | X | |
| Runtime D3 latency                                             | X | |
| Namespace Attribute Notices event                              | X | Log the event and trigger namespace reenumeration based on change log |
| Firmware Activation Notices event                              | X | Log the event and read the log page |
| Endurance Group Event Aggregate Log Page notices event         |   | |
| Controller Attributes                                          | X | Non-operational Power State Permissive Mode and NVM Sets are checked and used |
| NVM Sets                                                       | X | |
| FRU Globally Unique Identifier                                 |   | |
| Security Send/Security Receive Support                         | X | |
| Format NVM Support                                             | X | Supported through SCSI sanitize |
| NVMe-MI Send and NVMe-MI Receive                               | X | Supported through IOCTL_STORAGE_PROTOCOL_COMMAND in WinPE mode |
| Doorbell Buffer Config Support                                 |   | |
| Abort Command Support with Specified Limits                    |   | |
| Asynchronous Event Request Support                             | X | Supports limited to event count of 4 |
| SMART Log Page Support                                         | X | Supports log page per Namespace |
| Command Supported and Effects Log Page Support                 | X | Checked for vendor specific command execution |
| Extended Data for Log Page                                     | X | Supported through IOCTL_STORAGE_QUERY_PROPERTY |
| Persistent Event Log Support                                   |   | |
| Firmware Activation maximum time support                       |   | Currently not supported even though firmware activation without reset is supported |
| Firmware Update Granularity                                    | X | |
| Keep Alive Support                                             |   | |
| Temperature Report                                             | X | WCTEMP and CCTEMP. Accessible though IOCTL_STORAGE_QUERY_PROPERTY |
| Multiple Namespaces                                            | X | Supports runtime enumeration of namespaces |
| Compare Command                                                | X | Supported through IOCTL_STORAGE_PROTOCOL_COMMAND in WinPE mode |
| Write Uncorrectable Command                                    |   | |
| Dataset Management Command                                     | X | |
| Write Zeroes                                                   |   | |
| Set Features Save Option                                       | X | Currently only used for VWC persistent setting |
| Timestamp                                                      | X | |
| Verify Command                                                 |   | |
| Fused Operations (Compare and Write)                           |   | |
| Volatile Write Cache                                           | X | |
| Atomic Write Unit Normal                                       |   | |
| NVMe Qualified Names                                           |   | |
| Namespace Thinprovisioning                                     | X | |
| NVMe Boot                                                      | X | |
| Controller Fatal Status Condition                              | X | Log the event and continue with controller re-initialization |
--->

## <a name="reference-links"></a>引用链接
- [使用 NVMe 设备](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices)
- [NVMe 存储协议数据类型](https://docs.microsoft.com/windows/win32/api/winioctl/ne-winioctl-storage_protocol_nvme_data_type)
