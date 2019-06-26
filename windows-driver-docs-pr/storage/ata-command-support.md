---
title: ATA 命令支持
description: ATA 命令支持
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f417f9554e0872730dc1c4e4cf52bbf40868ba2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368409"
---
# <a name="ata-command-support"></a>ATA 命令支持


如果存储设备支持 ATA 命令集，StorPort 将直接向使用 ATA 传递控制代码的目标设备发送 ATA 命令。 设备管理应用程序可以使用[ **IOCTL\_ATA\_传递\_THROUGH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through)并[ **IOCTL\_ATA\_传递\_THROUGH\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct)控制代码实现此目的。

本部分包含有关用于颁发某些 ATA 命令请求的特殊要求的信息。

[安全组的命令](security-group-commands.md)

 

 




