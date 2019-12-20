---
title: StorNVMe 支持的 NVMe 功能
description: StorNVMe 支持的 NVMe 功能
ms.assetid: 96b62fbb-bcf3-402d-ba29-0a61dc95c92c
ms.date: 12/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 250ef95374d2f1c7a8a6c2a5866171cddfa3873e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252082"
---
# <a name="nvme-features-supported-by-stornvme"></a>StorNVMe 支持的 NVMe 功能

下表列出了 NVME 功能，指示每项功能是必需的还是可选的，并指示**StorNVMe**是否支持该功能。

| 功能  | 可选 | Mandatory | 支持 | 备注 |
| :------- | :------: | :-------: | :-------: | :------- |
| 固件提交/下载                                       |   | X | X | 支持第1个槽，多个槽。 与控制器报告的固件更新粒度对齐 |
| 固件激活而不重置                              | X |   | X | |
| 元数据处理                                              | X |   |   | |
| 端到端数据保护                                     | X |   |   | |
| 电源管理支持                                       |   | X | X | 支持非操作电源状态 |
| 自治电源状态转换                             | X |   | X | 支持 APST，但在默认情况下处于禁用状态。 可以通过注册表设置 IdlePowerMode = 3 启用 |
| D3 支持                                                     | X |   | X | 支持 D3 转换，但默认情况下禁用。 可以通过注册表设置 IdlePowerMode = 2 来启用 |
| 运行时 D3 转换                                         | X |   | X | 默认为新式备用中的选定平台启用 |
| 主机控制热量管理                             | X |   | X | 通过 IOCTL_STORAGE_QUERY_PROPERTY 获取功能，并通过 IOCTL_STORAGE_SET_PROPERTY 设置功能 |
| 虚拟化增强功能                                    | X |   |   | |
| 软件仿真的 Doorbell 步幅                         |   | X |   | |
| 标准供应商特定命令格式                        |   | X |   | |
| 预订                                                   | X |   |   | |
| 主机内存缓冲区支持                                     | X |   | X | |
| 重播受保护的内存块支持                          | X |   |   | |
| 设备自检                                               | X |   | X | 通过 IOCTL_STORAGE_PROTOCOL_COMMAND 支持 |
| 命名空间管理/附件命令支持                  | X |   | X | 在 WinPE 模式下通过 IOCTL_STORAGE_PROTOCOL_COMMAND 支持 |
| 启动分区                                                | X |   |   | |
| 遥测主机/控制器启动的日志页支持           | X |   | X | 通过 IOCTL_SCSI_PASS_THROUGH 将命令 SCSIOP_READ_DATA_BUFF16 与缓冲模式结合使用来支持 READ_BUFFER_MODE_ERROR_HISTORY |
| 净化操作                                            | X |   |   | |
| 读取恢复级别                                            | X |   |   | |
| 耐用性组                                               | X |   | X | 可以通过 IOCTL_STORAGE_QUERY_PROPERTY 检索信息 |
| 可预测延迟模式                                       | X |   |   | |
| 命名空间写保护                                     | X |   |   | |
| 非对称命名空间访问报告                          | X |   |   | |
| 获取 LBA 状态                                                 | X |   |   | |
| SQ 关联                                                | X |   |   | |
| 特定于供应商的信息的 Uuid                          | X |   |   | |
| 命名空间最佳 IO 边界                                  | X |   | X | |
| 通过 i/o 大小和一致性来提高性能 | X |   |   | 当前不支持 NPWG、NPWA、NPDG、NPDA 和 NOWS |
| Using                                                     | X |   | X | 支持流和标识指令 |
|                                                                |   |   |   | |
| 版本相容性                                             |   | X | X | 版本 < 的符合性 = 1。4 |
| 建议的仲裁突发                                  |   | X | X | 用户可以通过注册表项 ArbitrationBurst 设置除控制器报告值以外的任何值。 |
| 控制器多路径 IO                                       | X |   |   | |
| 命名空间共享功能                                 | X |   |   | |
| 最大数据传输大小支持                             | X |   | X | |
| 运行时 D3 延迟                                             | X |   | X | |
| 命名空间属性通知事件                              | X |   | X | 基于更改日志记录事件和触发命名空间 reenumeration |
| 固件激活通知事件                              | X |   | X | 记录事件并读取日志页 |
| 耐用性组事件聚合日志页面通知事件         | X |   |   | |
| 控制器属性                                          | X |   | X | 选中并使用了非操作电源状态权限模式和 NVM 集 |
| NVM 集                                                       | X |   | X | |
| FRU 全局唯一标识符                                 | X |   |   | |
| 安全发送/安全接收支持                         | X |   | X | |
| 格式 NVM 支持                                             | X |   | X | 通过 SCSI 净化支持 |
| NVMe-英里发送和 NVMe-英里接收                               | X |   | X | 在 WinPE 模式下通过 IOCTL_STORAGE_PROTOCOL_COMMAND 支持 |
| Doorbell Buffer Config 支持                                 | X |   |   | |
| 中止具有指定限制的命令支持                    |   | X |   | |
| 异步事件请求支持                             |   | X | X | 支持限制为事件计数4 |
| 智能日志页面支持                                         | X |   | X | 支持每个命名空间的日志页 |
| 命令支持和影响日志页支持                 | X |   | X | 检查特定于供应商的命令执行 |
| 日志页面的扩展数据                                     | X |   | X | 通过 IOCTL_STORAGE_QUERY_PROPERTY 支持 |
| 持久事件日志支持                                   | X |   |   | |
| 固件激活最大时间支持                       | X |   |   | 当前不受支持，即使支持无需重置的固件激活 |
| 固件更新粒度                                    | X |   | X | |
| 保持活动支持                                             | X |   |   | |
| 温度报表                                             |   | X | X | WCTEMP 和 CCTEMP。 可访问 IOCTL_STORAGE_QUERY_PROPERTY |
| 多个命名空间                                            | X |   | X | 支持命名空间的运行时枚举 |
| 比较命令                                                | X |   | X | 在 WinPE 模式下通过 IOCTL_STORAGE_PROTOCOL_COMMAND 支持 |
| 写入无法纠正的命令                                    | X |   |   | |
| 数据集管理命令                                     | X |   | X | |
| 写零                                                   | X |   |   | |
| 设置功能保存选项                                       | X |   | X | 目前仅用于 VWC 永久性设置 |
| 时间戳                                                      | X |   | X | |
| Verify 命令                                                 | X |   |   | |
| 带保险丝的操作（比较和写入）                           | X |   |   | |
| 可变写入缓存                                           | X |   | X | |
| 原子写入单元正常                                       | X |   |   | |
| NVMe 限定名称                                           | X |   |   | |
| 命名空间 Device.storage.hd.thinprovisioning                                     | X |   | X | |
| NVMe 引导                                                      |   | X | X | |
| 控制器严重状态条件                              | X |   | X | 记录事件，并继续执行控制器重新初始化 |
