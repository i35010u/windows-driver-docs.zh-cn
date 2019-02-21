---
title: 运行短信接收到的新后台事件
description: 运行短信接收到的新后台事件
ms.assetid: 57534569-3678-4e2c-b55a-7dc6f057fb7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3196d69f70e3e044915a21d30c0bfa076e9e372
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522291"
---
# <a name="run-new-sms-received-background-events"></a>运行短信接收到的新后台事件


移动宽带短信平台的新接收，具体取决于是否管理短信通知从移动网络运营商或常规短信的短信数据提供单独的系统事件。 新的管理短信通知从移动网络运营商收到的后台系统事件才可由移动宽带应用访问。

应用必须已获得用户同意的情况下使用短信以进行读取后台任务中的新接收的 SMS 消息。 应用无法读取后台任务，如果他们正在首次访问 SMS，因为该应用无法触发系统 SMS 设备从新的接收 SMS 消息的内容通过后台任务的同意提示。

下面的代码示例演示了专为运行接收新的 SMS 消息时的后台任务。

**C#后台任务代码**

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

**JavaScript 应用程序代码以注册后台任务**

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






