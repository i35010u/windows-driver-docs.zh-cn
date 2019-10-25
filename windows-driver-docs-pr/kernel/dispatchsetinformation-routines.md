---
title: DispatchSetInformation 例程
description: DispatchSetInformation 例程
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords:
- 调度例程 WDK 内核，DispatchSetInformation 例程
- DispatchSetInformation 例程
- 设置信息发送例程 WDK 内核
- IRP_MJ_SET_INFORMATION i/o 函数代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb899ab163f1fdef95e31e2c6d9d967e6a7a2998
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836831"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation 例程





驱动程序的[*DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程处理[**irp\_MJ\_集的 irp\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)i/o 函数代码。 此 i/o 函数代码的驱动程序支持是可选的，通常出现在较高级别的或文件系统驱动程序中。 此请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用[**SetEndOfFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-setendoffile)时，以及当内核模式组件调用[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)时发送。

 

 




