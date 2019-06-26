---
title: DispatchSetInformation 例程
description: DispatchSetInformation 例程
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords:
- 调度例程 WDK 内核，DispatchSetInformation 例程
- DispatchSetInformation 例程
- 设置信息的调度例程 WDK 内核
- IRP_MJ_SET_INFORMATION I/O 函数代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc2bc374abc5ff464a69c18d55b0f9ad5da67ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384970"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation 例程





驱动程序的[ *DispatchSetInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_设置\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information) I/O 函数代码。 此 I/O 函数代码的驱动程序支持是可选的并通常显示在更高级别的或文件系统驱动程序。 此请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 例如，发送时在用户模式应用程序调用[ **SetEndOfFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-setendoffile)，并在调用内核模式组件[ **ZwSetInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile).

 

 




