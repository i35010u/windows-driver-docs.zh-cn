---
title: DispatchQueryInformation 例程
description: DispatchQueryInformation 例程
ms.assetid: dfcb8ad0-ae95-4dd7-b4c8-a2f3ad4b12ef
keywords:
- 调度例程 WDK 内核，DispatchQueryInformation 例程
- DispatchQueryInformation 例程
- IRP_MJ_QUERY_INFORMATION I/O 函数代码
- 查询信息调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccd4b3f0c6c53e852a66a4dac2740d03a0d6524a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384986"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation 例程





驱动程序的[ *DispatchQueryInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information) I/O 函数代码。 此 I/O 函数代码的驱动程序支持是可选的并通常显示在更高级别的或文件系统驱动程序。 此请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 例如，发送时在用户模式应用程序调用[ **GetFileInformationByHandle**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getfileinformationbyhandle)，并在调用内核模式组件[ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile).

 

 




