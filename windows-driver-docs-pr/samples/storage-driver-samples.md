---
title: 存储驱动程序示例
description: 此目录中的存储驱动程序示例编写你的设备的自定义驱动程序提供一个起始点。
ms.assetid: 4FEB911D-78D5-403E-91AB-8A064E31F4FA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1826460c27c89f359a14929d6027db13950d8b89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374211"
---
# <a name="storage-driver-samples"></a>存储驱动程序示例


此目录中的驱动程序示例编写你的设备的自定义驱动程序提供一个起始点。

## <a name="storage"></a>存储


| 示例名称                                 | 解决方案                                                     | 描述                                                                                                                                                                                                                                     |
|---------------------------------------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CDROM 类驱动程序                          | [cdrom](https://go.microsoft.com/fwlink/p/?LinkId=617971)     | CD ROM 类驱动程序用于提供到 CD、 DVD 和蓝光驱动器的访问权限。 它支持插、 电源管理和自动运行 （媒体更改通知）。                                                                          |
| Classpnp 会类驱动程序库               | [classpnp](https://go.microsoft.com/fwlink/p/?LinkId=617978)  | 库存储类驱动程序。 它简化了大部分支持插即用 (PnP)、 电源管理和其他功能所需的代码编写的存储类驱动程序。 此库使用磁盘、 CDROM 和磁带类驱动程序。 |
| 磁盘类驱动程序                           | [disk](https://go.microsoft.com/fwlink/p/?LinkId=617979)      | 对于磁盘设备类驱动程序。                                                                                                                                                                                                                |
| AddFilter 存储筛选器工具               | [addfilter](https://go.microsoft.com/fwlink/p/?LinkId=617980) | 一种命令行应用程序中添加和删除给定的驱动器或卷筛选器驱动程序。                                                                                                                                                    |
| iSCSI WMI 客户端                            | [iscsi](https://go.microsoft.com/fwlink/p/?LinkId=617981)     | 可以使用 iSCSICLI.exe 工具、 iSCSI 发起程序属性页、 WBEMTEST.exe 工具和自定义的 WMI 脚本进行测试 iSCSI 微型端口中的 WMI 实现。                                                               |
| LSI\_U3 StorPort 微型端口                   | [lsi\_u3](https://go.microsoft.com/fwlink/p/?LinkId=617982)   | 使用并行 SCSI 主机总线适配器或使用 LSI 53C 1010 SCSI ASIC 的主板上的解决方案使用适配器驱动程序。                                                                                                                  |
| StorAHCI StorPort 微型端口                  | [storahci](https://go.microsoft.com/fwlink/p/?LinkId=617983)  | 一个示例 ACHI Storport 微型端口驱动程序。                                                                                                                                                                                                         |
| 多路径 I/O (MPIO) DSM 示例             | [msdsm](https://go.microsoft.com/fwlink/p/?LinkId=620203)     | 若要构建一个供应商特定，设备特定模块 (DSM) 时，请遵循示例。 此示例 DSM 支持 iSCSI 和光纤通道设备。                                                                                                   |
| 超级软盘 (sfloppy) 存储类驱动程序 | [sfloppy](https://go.microsoft.com/fwlink/p/?LinkId=617989)   | 类驱动程序的超级软盘驱动器。                                                                                                                                                                                                    |
| SCSI 直通界面工具            | [spti](https://go.microsoft.com/fwlink/p/?LinkId=617990)      | 演示如何与使用直通 Ioctl 使用 DeviceIoControl API 的应用程序中从 SCSI 设备通信。                                                                                                          |

 

 

 




