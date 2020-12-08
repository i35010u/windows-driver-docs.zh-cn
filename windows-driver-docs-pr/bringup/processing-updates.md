---
title: 处理更新
description: 在应用了任何固件更新包 (的) 并随后重新启动系统后，Windows 操作系统加载程序会将所有固件负载 (文件（在此示例中为 "固件") ）加载到物理内存中。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3918f8d5abe90777bdb59d6e2860f65426f329
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783591"
---
# <a name="processing-updates"></a>处理更新


在应用了任何固件更新包 (的) 并随后重新启动系统后，Windows 操作系统加载程序会将所有固件负载 (文件（在此示例中为 " *固件* ") ）加载到物理内存中。 Windows OS 加载器使用每个更新的相应 ESRT 条目中的信息创建胶囊标头，该条目描述了在调用 UEFI UpdateCapsule 时要使用的 GUID 和标志。 在设置每个胶囊标头的 "标志" 字段时，Windows 操作系统加载程序始终会设置胶囊 \_ 标志 \_ \_ \_ ，并在重置和胶囊 \_ 标志 \_ 启动 \_ 重置时保持。 \_ \_ \_ \_ \_ 如果驱动程序包的 INF 中指定了胶囊标志，Windows 操作系统加载器还可能会为固件类型设备固件额外设置胶囊标志。 还可以在 INF 中指定专用胶囊标志，并在调用 UEFI UpdateCapsule 时将其添加到指定的

返回到 [ESRT 表定义](esrt-table-definition.md) 中的 ESRT 示例和固件资源更新驱动程序包 INF 示例在 [创作更新驱动程序包](authoring-an-update-driver-package.md)中，Windows OS 加载程序创建的用于传递到 UpdateCapsule 的胶囊标头如下所示。

| 字段            | 值              | 注释                                                 |
|------------------|--------------------|---------------------------------------------------------|
| CapsuleGuid      | {系统 \_固件 | 从相应的 ESRT 资源项的 FirmwareClass。 |
| HeaderSize       | …                  | 填充以页面对齐 *固件* 开头。              |
| Flags            | 0x50000            | 持久保存并启动、重置。                    |
| CapsuleImageSize | …                  | 胶囊标头大小 + *固件* 大小。       |

 

请注意，在此示例中，在 ESRT 表中定义的两个设备中仅有一个安装了新的固件资源更新驱动程序包。 如果为表2中的第二个设备编写固件资源更新驱动程序包，并将其安装在相应的固件资源设备上，则将创建另一个胶囊标头，如下所示：

| 字段            | 值              | 注释                                                                                                                                 |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| CapsuleGuid      | {设备 \_固件 | 从相应的 ESRT 资源项的 FirmwareClass。                                                                                 |
| HeaderSize       | …                  | 填充到页面对齐设备。箱开始。                                                                                                  |
| Flags            | 0x50000            | 通过相应的 ESRT 资源条目的 CapsuleFlags，保存并启动、重置和填充系统表，或0x8010。 |
| CapsuleImageSize | …                  | 胶囊标头大小 + 设备的大小。装箱.                                                                                           |

 

Windows 操作系统加载程序加载了所有挂起的固件更新并创建了所需的数据结构来描述它们后，它会在调用 ExitBootServices 之前调用 UpdateCapsule 运行时服务。

**注意**  当平台固件具有对包括存储设备在内的所有设备的独占控制权时，将在 ExitBootServices 之前调用 UpdateCapsule。 UpdateCapsule 的平台固件实现可以将固件更新负载保存到永久性存储中以暂存更新或支持恢复回滚。

 

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[即插即用设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[来自 UEFI 环境的设备 I/O](device-i-o-from-the-uefi-environment.md)  
[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  
[固件更新状态](firmware-update-status.md)  



