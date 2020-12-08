---
title: 运行收到短信后的新后台事件
description: 运行收到短信后的新后台事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31fbe81bc040405090d44c0fe36df8a0ce950cf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828501"
---
# <a name="run-new-sms-received-background-events"></a>运行收到短信后的新后台事件


移动宽带 SMS 平台为收到的新 SMS 数据提供单独的系统事件，具体取决于它是来自移动网络操作员的管理 SMS 通知还是常规 SMS 消息。 从移动网络操作员收到的新的管理短信通知的后台系统事件只能由移动宽带应用程序访问。

应用必须已收到用户同意才能使用 SMS 在后台任务中读取新接收的 SMS 消息。 如果应用程序第一次访问 SMS，则不能从后台任务读取新收到的短信消息的内容，因为应用无法从后台任务触发系统 SMS 设备同意提示。

下面的代码示例演示了一个设计为在收到新的短信时运行的后台任务。

**C # 后台任务代码**

``` syntax
namespace SmsBackgroundSample
{
  public sealed class SmsBackgroundTask : IBackgroundTask
  { 
    // The Run method is the entry point of a background task.

    public void Run(IBackgroundTaskInstance taskInstance)
    {
      // Associate a cancellation handler with the background task.

      taskInstance.Canceled += new BackgroundTaskCanceledEventHandler(OnCanceled);

      ManualResetEvent manualEventWaiter = new ManualResetEvent(false);
      manualEventWaiter.Reset();

      // Do the background task activity.

      DisplayToastAsync(taskInstance, manualEventWaiter);

      // Wait until the async operation is done. We need to do this else the background process will exit.
      manualEventWaiter.WaitOne(5000);

            Debug.Print("Background " + taskInstance.Task.Name + (" process ran"));

  }

  async void DisplayToastAsync(IBackgroundTaskInstance taskInstance, ManualResetEvent manualEventWaiter)
  {
    SmsReceivedEventDetails smsDetails = (SmsReceivedEventDetails)taskInstance.TriggerDetails;
    SmsBinaryMessage smsEncodedmsg = (SmsBinaryMessage) smsDetails.BinaryMessageMessage;
    SmsTextMessage smsTextMessage = Windows.Devices.Sms.SmsTextMessage.FromBinaryMessage(smsEncodedmsg);

    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(ToastTemplateType.ToastText02);
    XmlNodeList stringElements = toastXml.GetElementsByTagName("text");

    stringElements.Item(0).AppendChild(toastXml.CreateTextNode(smsTextMessage.From));
    stringElements.Item(1).AppendChild(toastXml.CreateTextNode(smsTextMessage.Body));

    ToastNotification notification = new ToastNotification(toastXml);
    ToastNotificationManager.CreateToastNotifier().Show(notification);

    manualEventWaiter.Set();
  }

}
```

**用于注册后台任务的 JavaScript 应用代码**

``` syntax
var triggerAway = new Windows.ApplicationModel.Background.SystemTrigger(Windows.ApplicationModel.Background.SystemTriggerType.smsReceived, false);
var builderAway = new Windows.ApplicationModel.Background.BackgroundTaskBuilder();

builderAway.setTrigger(triggerAway);
builderAway.taskEntryPoint = "HelloWorldBackground.BackgroundTask1";
builderAway.name = "Sms";

var taskAway = builderAway.register();
taskAway.addEventListener("progress", new ProgressHandler(taskAway).onProgress);
taskAway.addEventListener("completed", new CompleteHandler(taskAway).onCompleted);
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

 






