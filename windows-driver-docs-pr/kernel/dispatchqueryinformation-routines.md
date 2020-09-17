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
ms.openlocfilehash: fca27ae13465ce961bb11a4cbf2ccbd64be09fd1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717482"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation 例程





驱动程序的 [*DispatchQueryInformation*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 查询 \_ 信息**](./irp-mj-query-information.md) i/o 函数代码处理 irp。 此 i/o 函数代码的驱动程序支持是可选的，通常出现在较高级别的或文件系统驱动程序中。 此请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用 [**GetFileInformationByHandle**](/windows/win32/api/fileapi/nf-fileapi-getfileinformationbyhandle)时，以及当内核模式组件调用 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时发送。

 

