---
title: DispatchQueryInformation 例程
description: DispatchQueryInformation 例程
ms.assetid: dfcb8ad0-ae95-4dd7-b4c8-a2f3ad4b12ef
keywords:
- 调度例程 WDK 内核，DispatchQueryInformation 例程
- DispatchQueryInformation 例程
- IRP_MJ_QUERY_INFORMATION i/o 函数代码
- 查询信息发送例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d401c4e61c8c6e840682dc4fa1e847ea87daa02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836841"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation 例程





驱动程序的[*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程为[**irp\_MJ\_QUERY\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)I/o 函数代码处理 irp。 此 i/o 函数代码的驱动程序支持是可选的，通常出现在较高级别的或文件系统驱动程序中。 此请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用[**GetFileInformationByHandle**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getfileinformationbyhandle)时，以及当内核模式组件调用[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时发送。

 

 




