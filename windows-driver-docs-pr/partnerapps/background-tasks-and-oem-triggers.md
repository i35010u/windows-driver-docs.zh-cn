---
title: 后台任务和自定义触发器
description: 后台任务和自定义触发器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b19725770b743dea30c7d317c72c0e8869e53943
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812565"
---
# <a name="background-tasks-and-custom-triggers"></a>后台任务和自定义触发器


后台任务是 Windows 10 上用于在后台运行代码的一种方法。 它们是标准应用程序平台的一部分，实质上是提供一个应用程序，该应用程序可以注册系统事件 (触发器) 以及该事件发生的时间在后台运行预定义的代码块。 系统触发器包括网络连接或系统时区更改等事件。

在某些情况下，提供的系统触发器不足以解决合作伙伴的情况。 **启动 Windows 10 版本 1803**，为合作伙伴提供更大的灵活性，并在更多情况下允许使用后台任务，合作伙伴可以创建应用可以注册的自定义触发器。 自定义触发器是在设备驱动程序中定义的，可用于为任何想要的硬件条件引发事件。 引发自定义触发器时，应用程序可以采用与标准应用模型完全相同的方式来执行后台任务。

## <a name="span-idimplementing_a_custom_triggerspanspan-idimplementing_a_custom_triggerspanspan-idimplementing_a_custom_triggerspanimplementing-a-custom-trigger"></a><span id="Implementing_a_custom_trigger"></span><span id="implementing_a_custom_trigger"></span><span id="IMPLEMENTING_A_CUSTOM_TRIGGER"></span>实现自定义触发器


实现自定义触发器需要执行两个步骤。 具体而言，必须在设备驱动程序或系统服务中定义和引发触发器，必须创建具有后台任务的应用程序。

### <a name="span-idcreating_the_custom_triggerspanspan-idcreating_the_custom_triggerspanspan-idcreating_the_custom_triggerspancreating-the-custom-trigger"></a><span id="Creating_the_custom_trigger"></span><span id="creating_the_custom_trigger"></span><span id="CREATING_THE_CUSTOM_TRIGGER"></span>创建自定义触发器

自定义触发器通过 **RtlRaiseCustomSystemEventTrigger** 函数在本机服务或设备驱动程序中定义和引发。 然后，可以从通用应用程序中注册该应用程序，并使用与系统定义的触发器相对相同的方式来启动后台任务。

下面的代码摘录说明了如何引发自定义触发器。

``` syntax
#define GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID L"{9118718B-FF80-4AFE-BAF1-D88A4525F3AB}"

CUSTOM_SYSTEM_EVENT_TRIGGER_CONFIG triggerConfig;
CUSTOM_SYSTEM_EVENT_TRIGGER_INIT(&triggerConfig,
                                 GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID);

NTSTATUS status = RtlRaiseCustomSystemEventTrigger(&triggerConfig);
```

在上面的代码示例中，作为参数传递给 **RtlRaiseCustomSystemEventTrigger** 函数的 GUID 定义应用程序在创建后台任务时将注册的触发器的标识符。 此标识符必须是唯一的。

### <a name="span-idcreating_a_background_taskspanspan-idcreating_a_background_taskspanspan-idcreating_a_background_taskspancreating-a-background-task"></a><span id="Creating_a_background_task"></span><span id="creating_a_background_task"></span><span id="CREATING_A_BACKGROUND_TASK"></span>创建后台任务

创建后台任务并为其注册自定义触发器非常类似于用于处理标准系统触发器的后台任务的过程。

1.  首先创建一个 UWP 应用。

2.  在应用程序清单文件中定义后台任务，如下面的示例中所示。 请注意， **Task** 元素的 **Type** 属性设置为`“systemEvent”`

    ``` syntax
    <Applications>
      <Application Id="MyBackgroundTaskSample.App" Executable="$targetnametoken$.exe" EntryPoint=" MyBackgroundTaskSample.App">
        <Extensions>
          <Extension Category="windows.backgroundTasks" EntryPoint="MyBackgroundTask.SampleBackgroundTask">
            <BackgroundTasks>
              <Task Type="systemEvent" />
            </BackgroundTasks>
          </Extension>
        </Extensions>
      </Application>
    </Applications>
    ```

3.  注册应用程序以侦听你创建的自定义触发器，如以下代码摘录中所示。 请注意，在实例化 **CustomSystemEventTrigger** 时使用的字符串必须与在本机服务或设备驱动程序中创建触发器时使用的 GUID 匹配。

    ``` syntax
    public void InitBackgroundTask()
    {
       // Create a new background task builder.
       BackgroundTaskBuilder taskBuilder = new BackgroundTaskBuilder();

       // Create a new CustomSystemEvent trigger.
       var myTrigger = new CustomSystemEventTrigger(
                            "{9118718B-FF80-4AFE-BAF1-D88A4525F3AB}", //Trigger Identifier
                            CustomSystemEventTriggerRecurrence.Once); //OneShot 

       // Associate the CustomSystemEvent trigger with the background task builder.
       taskBuilder.SetTrigger(myTrigger);

       // Specify the background task to run when the trigger fires.
       taskBuilder.TaskEntryPoint = MyBackgroundTask.SampleBackgroundTask;

       // Name the background task.
       taskBuilder.Name = “fabrikam.audio-jack.connected Task”;

       // Register the background task.
       BackgroundTaskRegistration taskRegistration = taskBuilder.Register();

       // Associate completed event handler with the new background task.
       taskRegistration.Completed += new BackgroundTaskCompletedEventHandler(OnCompleted); 
    }
    ```

4.  创建后台任务，如以下代码摘录中所示。

    ``` syntax
    namespace MyBackgroundTask
    {
       public sealed class SampleBackgroundTask : IBackgroundTask
       {
          // Called by the system when it's time to run our task
          public void Run(IBackgroundTaskInstance instance)
          {
             DoWork();
          }
       }
    }
    ```

有关创建、配置和使用后台任务和触发器的其他指南，请参阅 [快速入门：创建并注册后台任务](/previous-versions/windows/apps/hh977055(v=win.10))。

 

