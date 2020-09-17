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
ms.openlocfilehash: 35381076fa99b06c54890659c0533d525e427345
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716876"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation 例程





驱动程序的 [*DispatchSetInformation*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 集 \_ 信息**](./irp-mj-set-information.md) i/o 函数代码处理 irp。 此 i/o 函数代码的驱动程序支持是可选的，通常出现在较高级别的或文件系统驱动程序中。 此请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用 [**SetEndOfFile**](/windows/win32/api/fileapi/nf-fileapi-setendoffile)时，以及当内核模式组件调用 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)时发送。

 

