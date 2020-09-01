---
title: ATA 命令支持
description: ATA 命令支持
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaac7532e36793cf4aa0cc0baa5ff04f7fa45479
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192899"
---
# <a name="ata-command-support"></a>ATA 命令支持


如果存储设备支持 ATA 命令集，则 StorPort 会使用 ATA 直通控制代码将 ATA 命令直接发送到目标设备。 设备管理应用程序可以使用 [**ioctl \_ ata \_ 直通 \_ **](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through) 和 [**ioctl \_ ata \_ pass \_ 通过 \_ 直接**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct) 控制代码实现此目的。

本部分包含有关发出某些 ATA 命令请求的特殊要求的信息。

[安全组命令](security-group-commands.md)

 

