---
title: SCSI 驱动程序
description: SCSI 驱动程序
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70706845b4bec3cb4203dd83632c33d03c1f4260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840750"
---
# <a name="scsi-driver"></a>SCSI 驱动程序





SCSI 总线的内核模式静止映像驱动程序通过创建包含 SCSI **Read**命令的命令描述符块（CDB）支持**ReadFile** 。 它通过创建包含 SCSI **Write**命令的 CDB 来支持**WriteFile** 。 用户模式微型驱动程序可以通过调用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)来指定自定义的 CDBs。 有关详细信息，请参阅[SCSI 静止图像 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)。 有关**ReadFile**和**WriteFile**的说明，请参阅 Microsoft Windows SDK 文档。

 

 




