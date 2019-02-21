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
ms.openlocfilehash: 17970f99a883ff1a2488370da303f65e68acf3e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533619"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation 例程





驱动程序的[ *DispatchQueryInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_查询\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550788) I/O 函数代码。 此 I/O 函数代码的驱动程序支持是可选的并通常显示在更高级别的或文件系统驱动程序。 此请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 例如，发送时在用户模式应用程序调用[ **GetFileInformationByHandle**](https://msdn.microsoft.com/library/windows/desktop/aa364952)，并在调用内核模式组件[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052).

 

 




