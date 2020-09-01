---
title: 作业管理
description: Windows 8.1 和更高版本的 Windows 中引入了作业管理功能，可提供作业队列的实时视图。
ms.assetid: D1236DD2-D4AD-4615-9036-7EC75D6CADCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c34e1becfabf519aa3d3cc60b917673d72a6b66c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210033"
---
# <a name="job-management"></a>作业管理


Windows 8.1 和更高版本的 Windows 中引入了作业管理功能，可提供作业队列的实时视图。

此功能还允许客户端取消打印作业。 客户端可以从 UWP 设备应用或打印机扩展中调用相应的编程接口。

## <a name="the-new-interfaces"></a>新接口


Windows 8.1 中引入了以下接口来实现作业管理功能。

[**IPrinterQueue2**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)

[**IPrinterQueueView**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)

[**IPrinterQueueViewEvent**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)

[**IPrintJob**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)

[**IPrintJobCollection**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)

## <a name="initiating-a-job-management-session"></a>启动作业管理会话


若要启动作业管理会话，你必须首先指定并请求你要管理的一系列作业。 这一范围的作业称为 "视图"，可以使用 [**IPrinterQueue2：： GetPrinterQueueView**](/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue2-getprinterqueueview) 方法来指定它。

如果要更改视图以监视一组不同的作业，可以使用 [**IPrinterQueueView：： SetViewRange**](/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueueview-setviewrange) 方法执行此操作。

请注意，打印队列是动态队列。 因此，每次打印队列的状态发生更改时，都会触发事件， [**IPrinterQueueViewEvent：： OnChanged**](/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueueviewevent-onchanged) 方法会提供所请求视图的更新快照。

下面的 c # 代码段演示了如何使用新接口来启动作业管理会话。

```csharp
void PerformJobManagement(IPrinterQueue2 queue)
{
    //
    // Create a printer queue view and specify the range of
    // print queue positions to be monitored
    //

    PrinterQueueView queueView = queue.GetPrinterQueueView(0, COUNT_JOBS_MONITORED);

    //
    // Add the event handler to the IPrinterQueueView object via the 
    // standard COM event model, the IConnectionPoint mechanism.
    //

    queueView.OnChanged += queueView_OnChanged;


    //
    // When a different range of print jobs needs to be monitored, 
    // reset/update the view.
    //

    queueView.SetViewRange(20, COUNT_JOBS_MONITORED);

}

//
// Create an event handler that is called when
// there is a change in the View
//
void queueView_OnChanged(
    IPrintJobCollection pcollection,
    uint ulviewOffset,
    uint ulviewSize,
    uint ulcountJobsInPrintQueue)
{
    foreach (IPrintJob job in pCollection)
    {
        UIDisplay(job.Name);
        UIDisplay(job.Id);
    }
}
```

UIDisplay 用于为向用户显示信息而开发的机制的通用名称。

另外，请注意，当添加第一个事件处理程序，并且在删除最后一个事件处理程序时，将停止作业枚举。

## <a name="related-topics"></a>相关主题
[**IPrinterQueue2**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)  
[**IPrinterQueueView**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)  
[**IPrinterQueueViewEvent**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)  
[**IPrintJob**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)  
[**IPrintJobCollection**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)