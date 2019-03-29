---
title: ATA 命令支持
description: ATA 命令支持
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cdf12efd15059012e3bd4019c3a82f9c2b0bfbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566314"
---
# <a name="ata-command-support"></a>ATA 命令支持


如果存储设备支持 ATA 命令集，StorPort 将直接向使用 ATA 传递控制代码的目标设备发送 ATA 命令。 设备管理应用程序可以使用[ **IOCTL\_ATA\_传递\_THROUGH** ](https://msdn.microsoft.com/library/windows/hardware/ff559309)并[ **IOCTL\_ATA\_传递\_THROUGH\_直接**](https://msdn.microsoft.com/library/windows/hardware/ff559315)控制代码实现此目的。

本部分包含有关用于颁发某些 ATA 命令请求的特殊要求的信息。

[安全组的命令](security-group-commands.md)

 

 




