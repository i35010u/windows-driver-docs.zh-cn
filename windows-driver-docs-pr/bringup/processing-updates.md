---
title: 处理更新
description: 在已应用程序包任何固件更新并随后重新启动系统，Windows OS 加载程序加载所有固件有效负载文件 (在此示例中，firmware.bin) 到物理内存。
ms.assetid: 87BC1366-F69D-412A-883E-861853A4902A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b554d462080271a0886272ccbeed1a09d57d33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337400"
---
# <a name="processing-updates"></a>处理更新


在已应用程序包任何固件更新并随后重新启动系统，Windows OS 加载程序加载所有固件有效负载文件 (在此示例中， *firmware.bin*) 到物理内存。 在 Windows 操作系统加载程序创建封装标头使用的每个更新的相应 ESRT 项时，它描述了 GUID 和标志调用 UEFI UpdateCapsule 时要使用的信息。 在设置每个封装标头 flags 字段时，Windows OS 加载程序始终设置 CAPSULE\_标志\_PERSIST\_先行\_重置和封装\_标志\_启动\_重置。 此外，Windows OS 加载程序可能会设置 CAPSULE\_标志\_POPULATE\_系统\_固件的表类型设备\_固件，如果驱动程序包 INF 中指定了封装的标志。 在 INF 和指定时，还可以指定标志的专有 capsule 此外时，将包含调用 UEFI UpdateCapsule

返回引用中的 ESRT 示例[ESRT 表定义](esrt-table-definition.md)以及中的固件资源更新驱动程序 INF 包示例[创作更新驱动程序包](authoring-an-update-driver-package.md)，封装标头的 Windows 操作系统加载程序创建到进入 UpdateCapsule 会按如下所示。

| 字段            | 值              | 备注                                                 |
|------------------|--------------------|---------------------------------------------------------|
| CapsuleGuid      | {SYSTEM\_固件} | 从相应 ESRT 资源条目 FirmwareClass。 |
| HeaderSize       | …                  | 填充页对齐*firmware.bin*开始。              |
| Flags            | 0x50000            | 在中，保持原样并启动、 重置。                    |
| CapsuleImageSize | …                  | Capsule 标头大小 + 的大小*firmware.bin*。       |

 

请注意，在此示例中只有一个 ESRT 中定义的两个设备表已安装新的固件资源更新驱动程序包。 如果固件资源更新驱动程序包已创作表 2 中的第二个设备，然后安装相应的固件资源设备上，将按如下所示创建第二个封装标头：

| 字段            | ReplTest1              | 备注                                                                                                                                 |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| CapsuleGuid      | {设备\_固件} | 从相应 ESRT 资源条目 FirmwareClass。                                                                                 |
| HeaderSize       | …                  | 填充页对齐设备。BIN 开始。                                                                                                  |
| Flags            | 0x50000            | 在中，保持原样并启动、 重置，和填充系统表，或与从相应 ESRT 0x8010 资源条目 CapsuleFlags。 |
| CapsuleImageSize | …                  | Capsule 标头大小 + 设备的大小。纸盒。                                                                                           |

 

Windows 操作系统加载程序已加载所有挂起的固件更新并创建必要的数据结构来描述它们后，然后调用 UpdateCapsule 运行时服务，在调用 ExitBootServices 之前。

**请注意**  平台固件在必须全权控制所有设备，包括存储设备时 UpdateCapsule ExitBootServices 之前调用。 UpdateCapsule 平台固件实现可以将保存固件更新负载到持久存储来暂存更新，或以支持恢复回滚。

 

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[Plug and play 设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[设备 I/O 从 UEFI 环境](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  



