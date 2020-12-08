---
title: ATA 命令支持
description: ATA 命令支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af60d11df5158f82eb0184286d01381ec5e3cde4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804783"
---
# <a name="ata-command-support"></a>ATA 命令支持


如果存储设备支持 ATA 命令集，则 StorPort 会使用 ATA 直通控制代码将 ATA 命令直接发送到目标设备。 设备管理应用程序可以使用 [**ioctl \_ ata \_ 直通 \_**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through) 和 [**ioctl \_ ata \_ pass \_ 通过 \_ 直接**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct) 控制代码实现此目的。

本部分包含有关发出某些 ATA 命令请求的特殊要求的信息。

[安全组命令](security-group-commands.md)

 

