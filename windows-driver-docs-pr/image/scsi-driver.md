---
title: SCSI 驱动程序
description: SCSI 驱动程序
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 088a3c14cb6d00f513284350aa03c12862c1c2d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374251"
---
# <a name="scsi-driver"></a>SCSI 驱动程序





内核模式下仍映像驱动程序的 SCSI 总线上支持**ReadFile**通过创建包括 SCSI 命令描述符块 (CDB)**读取**命令。 它支持**WriteFile**通过创建包含 SCSI CDB**编写**命令。 用户模式下微型驱动程序可以通过调用指定自定义的 Cdb [ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)。 有关详细信息，请参阅[SCSI 仍映像 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)。 请参阅 Microsoft Windows SDK 文档有关的说明**ReadFile**并**WriteFile**。

 

 




