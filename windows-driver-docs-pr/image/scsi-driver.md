---
title: SCSI 驱动程序
description: SCSI 驱动程序
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10af337182a63a149f3b446c4ab310300d52f059
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563902"
---
# <a name="scsi-driver"></a>SCSI 驱动程序





内核模式下仍映像驱动程序的 SCSI 总线上支持**ReadFile**通过创建包括 SCSI 命令描述符块 (CDB)**读取**命令。 它支持**WriteFile**通过创建包含 SCSI CDB**编写**命令。 用户模式下微型驱动程序可以通过调用指定自定义的 Cdb [ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)。 有关详细信息，请参阅[SCSI 仍映像 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff548003)。 请参阅 Microsoft Windows SDK 文档有关的说明**ReadFile**并**WriteFile**。

 

 




