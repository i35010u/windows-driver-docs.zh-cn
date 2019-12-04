---
title: 存储驱动程序示例
description: 此目录中的存储驱动程序示例提供了为设备编写自定义驱动程序的起点。
ms.assetid: 4FEB911D-78D5-403E-91AB-8A064E31F4FA
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: c5340cbba706e30c3e5ef49374de8ebabe5b6b75
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735257"
---
# <a name="storage-driver-samples"></a>存储驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义驱动程序的起点。

| 示例 | 描述 |
| --- | --- |
| [CDROM 类驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cdrom-storage-class-driver) | CD ROM 类驱动程序用于提供对 CD、DVD 和蓝光驱动器的访问。 它支持即插即用、电源管理和自动运行（媒体更改通知）。 |
| [ClassPnP 类驱动程序库](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/classpnp-storage-class-driver-library) | 库存储类驱动程序。 它简化了支持即插即用（PnP）、电源管理和其他功能所需的大多数代码的写入存储类驱动程序。 磁盘、CDROM 和磁带类驱动程序使用此库。 |
| [磁盘类驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/disk-class-driver) | 磁盘设备的类驱动程序。 |
| [AddFilter 存储筛选器工具](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/addfilter-storage-filter-tool) | 一个命令行应用程序，用于添加和删除给定驱动器或卷的筛选器驱动程序。 |
| [iSCSI WMI 客户端](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/iscsi-wmi-client) | ISCSI 小型端口中的 WMI 实现，可使用 Iscsicli.exe 工具、iSCSI 发起程序属性页、WBEMTEST 工具和自定义 WMI 脚本进行测试。 |
| [LSI_U3 StorPort 微型端口](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/lsi_u3-storport-miniport-driver) | 用于并行 SCSI 主机总线适配器或使用 LSI 53C1010 SCSI ASIC 的主板解决方案的适配器驱动程序。 |
| [StorAHCI StorPort 微型端口](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/storahci-storport-miniport-driver) | 示例 Storport ACHI 微型端口驱动程序。 |
| [多路径 i/o （MPIO） DSM 示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/multipath-io-mpio-dsm-sample)     | 构建特定于设备特定模块（DSM）时要遵循的示例。 此示例 DSM 支持 iSCSI 和光纤通道设备。 |
| [超级软盘（sfloppy）存储类驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/super-floppy-sfloppy-storage-class-driver) | 适用于超级软盘驱动器的类驱动程序。 |
| [SCSI 传递接口工具](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/scsi-pass-through-interface-tool) | 演示如何在使用 DeviceIoControl API 的应用程序中使用 pass IOCTLs 与 SCSI 设备通信。 |
