---
title: ATA 命令支持
description: ATA 命令支持
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db69a825af9f88de9fc29876061db43dfeaf012b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845108"
---
# <a name="ata-command-support"></a>ATA 命令支持


如果存储设备支持 ATA 命令集，则 StorPort 会使用 ATA 直通控制代码将 ATA 命令直接发送到目标设备。 设备管理应用程序可以使用[**ioctl\_ata\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through)通过和[**ioctl\_ATA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct)通过\_直接控制代码实现此目的。

本部分包含有关发出某些 ATA 命令请求的特殊要求的信息。

[安全组命令](security-group-commands.md)

 

 




