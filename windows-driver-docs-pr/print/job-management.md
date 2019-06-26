---
title: 作业管理
description: 在 Windows 8.1 和更高版本的 Windows 提供的作业队列的实时视图中引入了一种作业管理功能。
ms.assetid: D1236DD2-D4AD-4615-9036-7EC75D6CADCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17df3c678b8051b4eebbc3aafbf607f93522896c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377525"
---
# <a name="job-management"></a>作业管理


在 Windows 8.1 和更高版本的 Windows 提供的作业队列的实时视图中引入了一种作业管理功能。

此功能还允许客户端取消打印作业。 客户端可以调用的相应编程接口从 UWP 的设备应用内或从打印机扩展插件。

## <a name="the-new-interfaces"></a>新接口


在 Windows 8.1，若要实现作业管理功能中引入了以下接口。

[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)

[**IPrinterQueueView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueview)

[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueviewevent)

[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjob)

[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjobcollection)

## <a name="initiating-a-job-management-session"></a>启动作业管理会话


若要启动作业管理会话，必须先指定并请求你想要管理的作业的范围。 作业的此范围称为"视图"，则使用[ **IPrinterQueue2::GetPrinterQueueView** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueue2-getprinterqueueview)方法，以指定它。

如果你想要更改视图来监视一组不同的作业，则可以使用[ **IPrinterQueueView::SetViewRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueueview-setviewrange)方法来执行该操作。

请注意，打印队列的动态队列。 每次打印队列更改的状态，因此激发的事件和[ **IPrinterQueueViewEvent::OnChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueueviewevent-onchanged)方法提供的视图的已请求更新的快照。

以下C#代码片段演示如何使用新的接口用于启动作业管理会话。

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

使用 UIDisplay 开发用于向用户显示信息的机制有通用名称。

和另请注意，作业枚举启动时第一个事件处理程序添加和删除最后一个事件处理程序时停止。

## <a name="related-topics"></a>相关主题
[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)  
[**IPrinterQueueView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueview)  
[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueviewevent)  
[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjob)  
[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjobcollection)  



