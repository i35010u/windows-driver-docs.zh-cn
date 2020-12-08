---
title: SCSI 驱动程序
description: SCSI 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b198be744d030b0e87d139c7c1159801388ee66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839101"
---
# <a name="scsi-driver"></a>SCSI 驱动程序





SCSI 总线的内核模式静止映像驱动程序通过创建命令描述符块 (CDB) ，其中包括 SCSI **Read** 命令来支持 **ReadFile** 。 它通过创建包含 SCSI **Write** 命令的 CDB 来支持 **WriteFile** 。 用户模式微型驱动程序可以通过调用 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)来指定自定义的 CDBs。 有关详细信息，请参阅 [SCSI 静止图像 I/o 控制代码](/windows-hardware/drivers/ddi/_image/index)。 有关 **ReadFile** 和 **WriteFile** 的说明，请参阅 Microsoft Windows SDK 文档。

 

