---
title: SCSI 驱动程序
description: SCSI 驱动程序
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4b3c01cae5ab5a4173e00c3401e4bf7b31a50d6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192967"
---
# <a name="scsi-driver"></a>SCSI 驱动程序





SCSI 总线的内核模式静止映像驱动程序通过创建命令描述符块 (CDB) ，其中包括 SCSI **Read**命令来支持**ReadFile** 。 它通过创建包含 SCSI **Write**命令的 CDB 来支持**WriteFile** 。 用户模式微型驱动程序可以通过调用 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)来指定自定义的 CDBs。 有关详细信息，请参阅 [SCSI 静止图像 I/o 控制代码](/windows-hardware/drivers/ddi/_image/index)。 有关 **ReadFile** 和 **WriteFile**的说明，请参阅 Microsoft Windows SDK 文档。

 

