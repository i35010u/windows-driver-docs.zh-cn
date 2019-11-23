---
title: ATA 端口驱动程序支持例程
description: 介绍 ATA 端口驱动程序例程
ms.assetid: 59222e82-8abb-4ef6-b58d-f70470c2def0
keywords:
- ATA 驱动程序支持例程
- 存储 WDK
- 存储支持例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4c32831f8a3c324eeb648549220f0fb3d02e80d
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72256321"
---
# <a name="ata-port-driver-support-routines"></a>ATA 端口驱动程序支持例程

本页对系统提供的 ATA 端口驱动程序提供的支持例程进行分类。

有关 ATA 驱动程序微型端口例程的列表，请参阅[Ata 微型端口驱动程序](ata-miniport-drivers.md)。

## <a name="initialization-routine"></a>初始化例程

ATA 端口驱动程序提供以下初始化例程。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortInitializeEx** | 初始化端口和微型端口驱动程序。 |

## <a name="routines-for-pci-config-space-access"></a>用于 PCI 配置空间访问的例程

ATA 端口驱动程序提供以下例程来帮助你读取和修改设备的 PCI 配置空间的内容。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortGetBusData** | 从设备 PCI 配置空间内的指定位置检索数据。 |
| **AtaPortSetBusData** | 按指定的偏移量将数据存储在指定设备的 PCI 配置空间。 |
|

## <a name="routines-for-processing-io-requests"></a>处理 i/o 请求的例程

ATA 端口驱动程序提供了以下 i/o 请求处理支持例程。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortGetScatterGatherList** | 检索与此请求关联的散点/集合列表。 |
| **AtaPortGetPhysicalAddress** | 将虚拟地址范围转换为物理地址范围。 |
| **AtaPortGetDeviceBase** | 返回一个映射的逻辑基址，该地址用于与主机总线适配器（HBA）进行通信。 |
| **AtaPortGetUncachedExtension** | 分配由 CPU 和设备共享的未缓存的公共缓冲区。 |
| **AtaPortBuildRequestSenseIrb** | 生成并返回 SCSIOP_REQUEST_SENSE 操作代码的 IRB。 |
| **AtaPortReleaseRequestSenseIrb** | 释放使用**AtaPortBuildRequestSenseIrb**分配的请求 IRB。 |
| **AtaPortCompleteAllActiveRequests** | 完成指定设备的所有活动 IRBs。 |
| **AtaPortCompleteRequest** | 完成指示的 IRB。 |

## <a name="callback-routines"></a>回调例程

微型端口驱动程序使用多个例程来请求从端口驱动程序进行回调。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortRequestWorkerRoutine** | 请求工作线程例程。 |
| **AtaPortRequestSynchronizedRoutine** | 请求与中断服务例程（ISR）进行同步。 |
| **AtaPortControllerSyncRoutine** | 提供对在控制器上的所有通道之间共享的数据结构的同步访问。 |
| **AtaPortRequestTimer** | 请求计时器回调。 |

## <a name="routines-that-report-a-configuration-change"></a>报告配置更改的例程

以下例程启用微型端口驱动程序，通知 ATA 端口驱动程序对附加到通道的设备的配置所做的更改。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortBusChangeDetected** | 向端口驱动程序通知指定通道上的设备配置发生的更改。 |
| **AtaPortRequestPowerStateChange** | 请求指定设备的电源状态转换。 |

## <a name="routines-to-control-request-queues"></a>控制请求队列的例程

端口驱动程序为每个逻辑单元号（LUN）请求队列和每个通道保留一个请求队列。 微型端口驱动程序可以使用以下例程暂停和恢复不同的请求队列。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortDeviceBusy** | 通知端口驱动程序指示的设备忙。 |
| **AtaPortDeviceReady** | 通知端口驱动程序指示的设备已准备好接受新请求。 |

## <a name="utility-routines"></a>实用工具例程

以下例程是适用于微型端口驱动程序的常规实用工具支持功能。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortCopyMemory** | 将数据从一个位置复制到另一个位置。 |
| \* * AtaPortMoveMemory 例程 | 将数据从一个位置复制到另一个位置。 |
| **AtaPortConvertUlongToPhysicalAddress** | 将给定的 ULONG 地址转换为类型 IDE_PHYSICAL_ADDRESS 的值。 |
| **AtaPortConvertPhysicalAddressToUlong** | 将 IDE_PHYSICAL_ADDRESS 类型的地址截断到 ULONG。 |
| **AtaPortStallExecution** | 微型端口驱动程序中的停止。 |
| **AtaPortInitializeQueueTag** | 初始化指定设备的队列标记列表。 |
| **AtaPortAllocateQueueTag** | 返回指定设备的队列标记。 |
| **AtaPortReleaseQueueTag** | 释放指定的队列标记。 |

## <a name="debug-and-error-reporting-routines"></a>调试和错误报告例程

以下例程可用于调试和错误报告。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortDebugPrint** | 将消息字符串传递给内核调试器，以便调试器打印。 |

## <a name="routines-for-device-port-and-register-access"></a>用于设备端口和寄存器访问的例程

ATA 端口驱动程序提供以下端口并注册访问支持例程。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortReadPortBufferUchar** | 将给定数量的无符号字节值从 HBA 传输到缓冲区。 |
| **AtaPortReadPortBufferUlong** | 将给定数目的 ULONG 值从 HBA 传输到缓冲区。 |
| **AtaPortReadPortBufferUshort** | 将给定数量的 USHORT 值从 HBA 传输到缓冲区。 |
| **AtaPortReadPortUchar** | 从 HBA 读取无符号字节值。 |
| **AtaPortReadPortUlong** | 从 HBA 读取 ULONG 值。 |
| **AtaPortReadPortUshort** | 从 HBA 读取 USHORT 值。 |
| **AtaPortReadRegisterBufferUchar** | 将指定数量的无符号字节从 HBA 传输到缓冲区。 |
| **AtaPortReadRegisterBufferUlong** | 将指定数目的 ULONG 从 HBA 传输到缓冲区。 |
| **AtaPortReadRegisterBufferUshort** | 将指定数目的 USHORT 从 HBA 传输到缓冲区。 |
| **AtaPortReadRegisterUchar** | 从 HBA 读取无符号字节值。 |
| **AtaPortReadRegisterUlong** | 从 HBA 读取 ULONG 值。 |
| **AtaPortReadRegisterUshort** | 从 HBA 读取 USHORT 值。 |
| **AtaPortWritePortBufferUchar** | 将值写入指定的寄存器地址。 |
| **AtaPortWritePortBufferUlong** | 将值写入指定的寄存器地址。 |
| **AtaPortWritePortBufferUshort** | 将值写入指定的寄存器地址。 |
| **AtaPortWritePortUchar** | 将无符号字节值传输到 HBA。 |
| **AtaPortWritePortUlong** | 将 ULONG 值传输到 HBA。 |
| **AtaPortWritePortUshort** | 将 USHORT 值传输到 HBA。 |
| **AtaPortWriteRegisterBufferUchar** | 将指定数目的无符号字节从缓冲区传输到 HBA。 |
| **AtaPortWriteRegisterBufferUlong** | 将指定数目的 ULONG 值从缓冲区传输到 HBA。 |
| **AtaPortWriteRegisterBufferUshort** | 将指定数目的 USHORT 值从缓冲区传输到 HBA。 |
| **AtaPortWriteRegisterUchar** | 将无符号字节传输到 HBA 地址。 |
| **AtaPortWriteRegisterUlong** | 将 ULONG 值传输到 HBA 地址。 |
| **AtaPortWriteRegisterUshort** | 将 USHORT 值传输到 HBA 地址。|

## <a name="routines-for-registry-access"></a>注册表访问例程

实现通道接口的微型端口驱动程序可以调用以下例程来访问 Windows 注册表。 仅实现控制器接口例程的微型端口驱动程序无法访问这些例程。

| 例程 | 描述 |
| ------- | ----------- |
| **AtaPortRegistryAllocateBuffer** | 为注册表操作分配缓冲区。 |
| **AtaPortRegistryFreeBuffer** | 释放使用**AtaPortRegistryAllocateBuffer**分配的注册表缓冲区。 |
| **AtaPortRegistryControllerKeyRead** | 读取与注册表项 HKLM 上指定的值名称关联的数据\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*n*，其中*N*是控制器的编号。 |
| **AtaPortRegistryContrlollerKeyWrite** | 将数据写入到注册表项 HKLM\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*n*的指定值名称，其中*N*是控制器的编号。 |
| **AtaPortRegistryControllerKeyWriteDeferred** | 以异步方式将数据写入到注册表项 HKLM\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*n*，其中*N*是控制器的编号。 |
| **AtaPortRegistryChannelSubKeyRead** | 读取与注册表项 HKLM 上指定的值名称关联的数据\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*n*\Channel*M*，其中*N*是控制器的编号， *M*是通道的编号。 |
| **AtaPortRegistryChannelSubKeyWrite** | 将数据写入到注册表项 HKLM\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*N*\Channel*M*下指定的值名称，其中*N*是控制器的编号， *M*是通道的编号。 |
| **AtaPortRegistryChannelSubKeyWriteDeferred** | 将数据异步写入到注册表项 HKLM\\CurrentControlSet\\Services\\&lt;服务名称&gt;\Controller*N*\Channel*M*下的指定值名称，其中*N*是控制器的编号， *M*是通道的编号。 |
