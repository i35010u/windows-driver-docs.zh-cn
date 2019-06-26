---
title: 后台任务和自定义触发器
description: 后台任务和自定义触发器
ms.assetid: 672d3501-da84-495b-b70e-f07de32aff53
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b944e4b402de69be1e60fcb0c9ce1f5a8f0d3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353569"
---
# <a name="background-tasks-and-custom-triggers"></a>后台任务和自定义触发器


后台任务是一种方法可以在 Windows 10 上的在后台运行代码。 它们是标准的应用程序平台的一部分，实质上是为应用提供的注册系统事件 （触发器） 和该事件发生在后台运行预定义的代码块时的功能。 系统触发器包括事件，例如网络连接中的更改或系统时区。

在某些情况下，提供的系统触发器都不足以解决合作伙伴方案。 **从 Windows 10 版本 1803年**，以便为合作伙伴提供更大的灵活性和允许使用的后台任务的更多情况下，合作伙伴可以创建自定义触发器的应用可以注册。 自定义触发器定义中的设备驱动程序和可用于引发任何你想的硬件条件的事件。 当引发自定义触发器时，您的应用程序中作为标准应用程序模型完全相同的方式执行的后台任务。

## <a name="span-idimplementingacustomtriggerspanspan-idimplementingacustomtriggerspanspan-idimplementingacustomtriggerspanimplementing-a-custom-trigger"></a><span id="Implementing_a_custom_trigger"></span><span id="implementing_a_custom_trigger"></span><span id="IMPLEMENTING_A_CUSTOM_TRIGGER"></span>实现自定义的触发器


有两个步骤来实现自定义触发器。 具体而言，必须定义和设备驱动程序或系统服务内引发触发器，必须创建带有后台任务的应用程序。

### <a name="span-idcreatingthecustomtriggerspanspan-idcreatingthecustomtriggerspanspan-idcreatingthecustomtriggerspancreating-the-custom-trigger"></a><span id="Creating_the_custom_trigger"></span><span id="creating_the_custom_trigger"></span><span id="CREATING_THE_CUSTOM_TRIGGER"></span>创建自定义的触发器

定义数据并自定义触发器内的本机服务或设备驱动程序通过引发**RtlRaiseCustomSystemEventTrigger**函数。 它可为从通用应用注册和使用相同的方式相对为系统定义触发器启动的后台任务。

以下代码段说明了如何引发自定义触发器。

``` syntax
#define GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID L"{9118718B-FF80-4AFE-BAF1-D88A4525F3AB}"

CUSTOM_SYSTEM_EVENT_TRIGGER_CONFIG triggerConfig;
CUSTOM_SYSTEM_EVENT_TRIGGER_INIT(&triggerConfig,
                                 GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID);

NTSTATUS status = RtlRaiseCustomSystemEventTrigger(&triggerConfig);
```

在上面的代码示例中，GUID 作为参数传递给**RtlRaiseCustomSystemEventTrigger**函数定义的触发器的创建的后台任务时，应用程序将注册为标识符。 此标识符必须是唯一的。

### <a name="span-idcreatingabackgroundtaskspanspan-idcreatingabackgroundtaskspanspan-idcreatingabackgroundtaskspancreating-a-background-task"></a><span id="Creating_a_background_task"></span><span id="creating_a_background_task"></span><span id="CREATING_A_BACKGROUND_TASK"></span>创建的后台任务

创建的后台任务和注册的自定义触发器是用于使用标准系统触发器的后台任务的过程非常类似。

1.  首先，创建 UWP 应用。

2.  在应用程序清单文件中定义的后台任务，如下面的示例中所示。 请注意，**类型**的属性**任务**元素设置为 `“systemEvent”`

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

3.  注册应用以侦听以下代码段中所示创建的自定义触发器。 请注意，实例化时使用的字符串**CustomSystemEventTrigger**必须匹配项时使用的 GUID 在本地服务或设备驱动程序中创建触发器。

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

4.  创建的后台任务，如以下代码段中所示。

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

有关其他指南有关创建、 配置和使用后台任务和触发器，请参阅[快速入门：创建并注册后台任务](https://docs.microsoft.com/previous-versions/windows/apps/hh977055(v=win.10))。

 

 





