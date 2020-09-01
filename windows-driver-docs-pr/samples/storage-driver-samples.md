---
title: 存储驱动程序示例
description: 此目录中的存储驱动程序示例提供了为设备编写自定义驱动程序的起点。
ms.assetid: 4FEB911D-78D5-403E-91AB-8A064E31F4FA
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 42108d0514e894ec28f8bed76506bbc488e3c69e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190303"
---
# <a name="storage-driver-samples"></a>存储驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [CDROM 类驱动程序](/samples/microsoft/windows-driver-samples/cdrom-storage-class-driver) | CD ROM 类驱动程序用于提供对 CD、DVD 和蓝光驱动器的访问。 它支持即插即用、电源管理和自动运行 (媒体更改通知) 。 |
| [ClassPnP 类驱动程序库](/samples/microsoft/windows-driver-samples/classpnp-storage-class-driver-library) | 库存储类驱动程序。 它简化了在支持即插即用 (PnP) 、电源管理和其他功能所需的大多数代码的情况下写入存储类驱动程序。 磁盘、CDROM 和磁带类驱动程序使用此库。 |
| [磁盘类驱动程序](/samples/microsoft/windows-driver-samples/disk-class-driver) | 磁盘设备的类驱动程序。 |
| [AddFilter 存储筛选器工具](/samples/microsoft/windows-driver-samples/addfilter-storage-filter-tool) | 一个命令行应用程序，用于添加和删除给定驱动器或卷的筛选器驱动程序。 |
| [iSCSI WMI 客户端](/samples/microsoft/windows-driver-samples/iscsi-wmi-client) | 可使用 iSCSICLI.exe 工具、iSCSI 发起程序属性页、WBEMTEST.exe 工具和自定义 WMI 脚本测试的 iSCSI 小型端口中的 WMI 实现。 |
| [LSI_U3 StorPort 微型端口](/samples/microsoft/windows-driver-samples/lsi_u3-storport-miniport-driver) | 用于并行 SCSI 主机总线适配器或使用 LSI 53C1010 SCSI ASIC 的主板解决方案的适配器驱动程序。 |
| [StorAHCI StorPort 微型端口](/samples/microsoft/windows-driver-samples/storahci-storport-miniport-driver) | 示例 Storport ACHI 微型端口驱动程序。 |
| [多路径 i/o (MPIO) DSM 示例](/samples/microsoft/windows-driver-samples/multipath-io-mpio-dsm-sample)     |  (DSM) 生成特定于供应商的特定于设备的模块时要遵循的示例。 此示例 DSM 支持 iSCSI 和光纤通道设备。 |
| [超级软盘 (sfloppy) 存储类驱动程序](/samples/microsoft/windows-driver-samples/super-floppy-sfloppy-storage-class-driver) | 适用于超级软盘驱动器的类驱动程序。 |
| [SCSI 传递接口工具](/samples/microsoft/windows-driver-samples/scsi-pass-through-interface-tool) | 演示如何在使用 DeviceIoControl API 的应用程序中使用 pass IOCTLs 与 SCSI 设备通信。 |