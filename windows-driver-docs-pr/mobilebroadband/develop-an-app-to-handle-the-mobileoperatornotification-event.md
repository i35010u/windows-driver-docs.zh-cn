---
title: 开发用于处理 MobileOperatorNotification 事件的应用
description: 开发用于处理 MobileOperatorNotification 事件的应用
ms.assetid: 3c483888-8ec4-4270-af3e-ef1efc995171
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee194fd015736131c5a131e3630af724f7c714dc
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91755030"
---
# <a name="develop-an-app-to-handle-the-mobileoperatornotification-event"></a>开发用于处理 MobileOperatorNotification 事件的应用


本主题介绍如何开发用于处理 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件的移动宽带应用。

-   [最佳实践](#bp)

-   [步骤1：后台任务协定声明](#stepone)

-   [步骤2：后台任务处理程序](#steptwo)

-   [步骤3：处理激活事件](#stepthree)

-   [步骤4：处理后台任务完成处理程序](#stepfour)

-   [故障排除](#ts)

-   [示例 backgroundtask.js 文件](#samp)

## <a name="span-idbpspanspan-idbpspanbest-practices"></a><span id="bp"></span><span id="BP"></span>最佳做法


对于后台事件处理，应使用以下最佳做法：

-   不要注册无法执行操作的后台事件。 处理这些事件将不必要地使用应用配额。

-   请勿在收到后台事件时执行大量处理。

-   考虑将处理推迟到下一次启动应用程序时。

-   考虑显示 toast 通知并更新磁贴以响应后台事件。 移动宽带应用可以处理后台事件负载。

## <a name="span-idsteponespanspan-idsteponespanstep-1-background-task-contract-declaration"></a><span id="stepone"></span><span id="STEPONE"></span>步骤1：后台任务协定声明


为了使 Windows 能够识别移动宽带应用提供的后台任务体验，应用程序必须声明它提供的是系统功能的扩展。

若要在 Visual Studio 项目的 appxmanifest.xml 文件中进行声明，请执行以下步骤：

**声明后台任务协定**

1.  在 **解决方案资源管理器**中，双击项目的 appxmanifest.xml 文件。

2.  在 " **声明** " 选项卡上的 " **可用声明**" 中，选择 " **后台任务** "，然后单击 " **添加**"。

3.  在 " **属性** " 标题下，输入以下应用信息：

    -   在 "**应用设置**" 下的 "**起始页**" 框中，对于使用 JavaScript 和 HTML 的移动宽带应用，请输入用于处理应用中的后台任务的文件名 (例如**backgroundtask.js**) 。

    -   在 " **支持的任务类型** " 标题下，单击 " **系统事件** " 复选框。

如果正确完成此操作，则应在 appxmanifest.xml 文件中包含如下所示的扩展元素。

``` syntax
<Extension Category="windows.backgroundTasks" StartPage="backgroundtask.js">
  <BackgroundTasks>
    <Task Type="systemEvent" />
  </BackgroundTasks>
</Extension>
```

## <a name="span-idsteptwospanspan-idsteptwospanstep-2-background-task-handler"></a><span id="steptwo"></span><span id="STEPTWO"></span>步骤2：后台任务处理程序


如果你的应用程序提供移动运营商通知声明，则它必须为后台任务激活提供处理程序。 处理程序将从 [**windows.networking.networkoperators**](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails)中获取移动运营商网络帐户 ID 和事件数据。

由于后台任务支持的唯一 UI 是 **toast**，因此后台任务处理程序可以显示 toast 或将 [**NetworkOperatorNotificationEventDetails**](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails) 保存到本地存储中。

下面的代码示例演示了一个设计为在收到新的管理短信通知时运行的后台任务。

**C#**

``` syntax
using Windows.Networking.NetworkOperators;

namespace MNOMessageBackground
{
    public sealed class MNOBackgroundTask : IBackgroundTask
    {
       public void Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)
       {
         NetworkOperatorNotificationEventDetails notifyData = (NetworkOperatorNotificationEventDetails)taskInstance.TriggerDetails;

         //The network account ID is stored in notifyData.NetworkAccountId

            switch (notifyData.NotificationType)
            {
                case NetworkOperatorEventMessageType.Gsm: // 0
                    break;
                case NetworkOperatorEventMessageType.Cdma: // 1
                    break;
                case NetworkOperatorEventMessageType.Ussd: // 2
                    break;
                case NetworkOperatorEventMessageType.DataPlanThresholdReached: // 3
                    break;
                case NetworkOperatorEventMessageType.DataPlanReset: //4 
                    break;
                case NetworkOperatorEventMessageType.DataPlanDeleted: //5
                    break;
                case NetworkOperatorEventMessageType.ProfileConnected: //6
                    break;
                case NetworkOperatorEventMessageType.ProfileDisconnected: //7
                    break;
                case NetworkOperatorEventMessageType.RegisteredRoaming: //8
                    break;
                case NetworkOperatorEventMessageType.RegisteredHome: ///9
                    break;
                case NetworkOperatorEventMessageType.TetheringEntitlementCheck: //10
                    break;

                default:
                    break;
             }

            // Add code to save the message to app local storage, and optionally show toast notification and tile updates.
        }
    }
}
```

**JavaScript**

``` syntax
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,
        networkOperatorEventType = Windows.Networking.NetworkOperators.NetworkOperatorEventMessageType,
        key = null,
        settings = Windows.Storage.ApplicationData.current.localSettings;

    try {

        
        var details = backgroundTaskInstance.triggerDetails;

// The network account ID is stored in details.networkAccountId.

        switch (details.notificationType) {
            case networkOperatorEventType.gsm:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.cdma:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.ussd:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.dataPlanThresholdReached:
                showToast("Mobile Broadband message", "Data plan threshold reached");
                break;
            case networkOperatorEventType.dataPlanReset:
                showToast("Mobile Broadband message", "Data plan reset");
                break;
            case networkOperatorEventType.dataPlanDeleted:
                showToast("Mobile Broadband message", "Data plan deleted");
                break;
            case networkOperatorEventType.profileConnected:
                showToast("Mobile Broadband message", "Profile connected");
                break;
            case networkOperatorEventType.profileDisconnected:
                showToast("Mobile Broadband message", "Profile disconnected");
                break;
            case networkOperatorEventType.registeredRoaming:
                showToast("Mobile Broadband message", "Registered roaming");
                break;
            case networkOperatorEventType.registeredHome:
                showToast("Mobile Broadband message", "Registered home");
                break;
            case networkOperatorEventType.tetheringEntitlementCheck:
                showToast("Mobile Broadband message", "Entitlement check completed");
                break;
            default:
                showToast("Mobile Broadband message", "Unknown message");
                break;
        }

        //
        // A JavaScript background task must call close when it is done.
        //
 close();
    }
    catch (exception) {
// Display error message.
close();
    }
```

### <a name="span-idshow_tile_and_toast_notificationsspanspan-idshow_tile_and_toast_notificationsspanspan-idshow_tile_and_toast_notificationsspanshow-tile-and-toast-notifications"></a><span id="Show_tile_and_toast_notifications"></span><span id="show_tile_and_toast_notifications"></span><span id="SHOW_TILE_AND_TOAST_NOTIFICATIONS"></span>显示磁贴和 toast 通知

建议你在移动宽带应用中显示 toast 和磁贴通知，因为用户可能会因为其暂时性性质而错过 toast 通知。 有关 toast 通知和磁贴更新体验设计指南，请参阅 [设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)。

**启用 toast 通知**

1.  在 **解决方案资源管理器**中，双击项目的 appxmanifest.xml 文件。

2.  在 " **应用程序 UI** " 选项卡的 " **通知** " 标题下，将 " **支持 Toast** " 设置为 **"是"**。

如果正确完成此操作，则应在 appxmanifest.xml 文件中包含如下所示的扩展元素。

``` syntax
<VisualElements … ToastCapable="true"… />
```

下面的代码演示如何在后台任务句柄中显示 toast 通知：

**JavaScript**

``` syntax
function showToast(title, body) {
        var notifications = Windows.UI.Notifications;
        var toastNotificationManager = Windows.UI.Notifications.ToastNotificationManager;
        var toastXml = toastNotificationManager.getTemplateContent(notifications.ToastTemplateType.toastText02);

        var temp = "the parameter will pass to app when app activated from tap Toast ";
        toastXml.selectSingleNode("/toast").setAttribute("launch", temp);

        var textNodes = toastXml.getElementsByTagName("text");
        textNodes[0].appendChild(toastXml.createTextNode(title));
        textNodes[1].appendChild(toastXml.createTextNode(body));

        var toast = new notifications.ToastNotification(toastXml);
        toastNotificationManager.createToastNotifier().show(toast);
    }
```

### <a name="span-idget_sms_text_messagespanspan-idget_sms_text_messagespanspan-idget_sms_text_messagespanget-sms-text-message"></a><span id="Get_SMS_text_message"></span><span id="get_sms_text_message"></span><span id="GET_SMS_TEXT_MESSAGE"></span>获取短信消息

如果后台任务是由传入 SMS 消息触发的，则后台任务详细信息会在其负载中携带 SMS 对象。

**JavaScript**

``` syntax
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,

    try {
        
        var details = backgroundTaskInstance.triggerDetails;
        if (details.notificationType === networkOperatorEventType.gsm
        || details.notificationType === networkOperatorEventType.cdma)
        {
     var textMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(details.smsMessage);
            
         // textMessage can be used to get other SmsMessage properties    
         // like sender number, timestamp, message part count etc.
         showToast("From: " + textMessage.from + "; TimeStamp: " + textMessage.timestamp, details.message);
        }
```

### <a name="span-iduse_local_storagespanspan-iduse_local_storagespanspan-iduse_local_storagespanuse-local-storage"></a><span id="Use_local_storage"></span><span id="use_local_storage"></span><span id="USE_LOCAL_STORAGE"></span>使用本地存储

后台任务可以使用本地存储来保存从后台事件获取的消息，使应用可以在以后使用该信息。

**JavaScript**

``` syntax
    //
    // Save the message 
    //
    var settings = Windows.Storage.ApplicationData.current.localSettings;
    var keyMessage = "BA5857FA-DE2C-4A4A-BEF2-49D8B4130A39";


    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current;

    var details = backgroundTaskInstance.triggerDetails;
    settings.values[keyMessage] = details.message;
```

下面的代码演示如何检索应用程序中后台任务处理程序存储的消息：

**JavaScript**

``` syntax
var settings = Windows.Storage.ApplicationData.current.localSettings;
    var keyMessage = "BA5857FA-DE2C-4A4A-BEF2-49D8B4130A39";
    var operatorMessage = settings.values[keyMessage];
```

## <a name="span-idstepthreespanspan-idstepthreespanstep-3-handle-the-activation-event"></a><span id="stepthree"></span><span id="STEPTHREE"></span>步骤3：处理激活事件


如果 toast 设置了参数，它将通过 **详细信息**传递给应用。

在 JavaScript 或 c # 中，可以处理 [**onactivated**](/previous-versions/windows/apps/br212679(v=win.10)) 事件，然后检查传递到事件处理程序的事件参数。 从 toast 激活会传递类型为 [**WebUI. WebUILaunchActivatedEventArgs**](/uwp/api/Windows.UI.WebUI.WebUILaunchActivatedEventArgs)的事件参数。 如果事件参数的 **详细信息** 为 [**windows.applicationmodel.resources.core. ctivationKind**](/uwp/api/Windows.ApplicationModel.Activation.ActivationKind)。**启动**时，应用程序提供启动体验或通知体验，具体取决于事件参数的 **详细信息。 argument** 属性是否设置为 **null**。

**JavaScript**

``` syntax
WinJS.Application.addEventListener("activated", activated; false);

function activated(eventArgs)
{
  if (eventArgs.detail.kind == Windows.ApplicationModel.Activation.ActivationKind.launch)
  {
    if (!eventArgs.detail.arguments)
    {
      // Initialize logic for the Start experience here.
    }
    else
    {
      // Initialize logic for the Notification experience here.
    }
  }
}
```

## <a name="span-idstepfourspanspan-idstepfourspanstep-4-handle-background-task-completion-handlers"></a><span id="stepfour"></span><span id="STEPFOUR"></span>步骤4：处理后台任务完成处理程序


前台应用还可以注册在后台任务完成时通知完成处理程序。 完成状态或在后台任务的 **Run** 方法中发生的任何异常将传递到前台应用程序中的完成处理程序。 如果在任务完成时该应用程序被挂起，则它会在下次恢复应用程序时收到完成通知。 如果应用处于 **终止** 状态，则不会接收到完成通知。 如果后台任务需要保留已成功运行的信息，则它必须通过使用状态管理器或其他方法（例如，应用程序在返回到 **运行** 状态时可以读取的文件）来保存信息。

**重要提示**   尽管移动运营商背景事件由系统自动注册到应用程序，但应用程序仍需要至少运行一次，才能注册到后台完成或进度处理程序。

 

**C#**

``` syntax
foreach (var cur in BackgroundTaskRegistration.AllTasks)
{
   if(cur.Value.Name == “MobileOperatorNotificationHandler”)
   {
       cur.Value.Progress += new BackgroundTaskProgressEventHandler(OnProgress);
       cur.Value.Completed += new BackgroundTaskCompletedEventHandler(OnCompleted);
   }
}

//
// Handle background task completion.
private void OnCompleted(IBackgroundTaskRegistration sender, BackgroundTaskCompletedEventArgs e)
{
   var taskCompletion = task as IBackgroundTaskRegistration;
   var completionArgs = args.Context as BackgroundTaskCompletedEventArgs;
   
  //
  // If the background task threw an exception, display the exception in the error text box.
  if (completionArgs.Status != null)
  {
    throw completionArgs.Status;
  }
}

// Handle background task progress.
private void OnProgress(IBackgroundTaskRegistration sender, BackgroundTaskProgressEventArgs e)
{
  var taskRegistration = task as IBackgroundTaskRegistration;
  var progressArgs = args.Context as BackgroundTaskProgressEventArgs;
  // progressArgs.Progress has the progress percentage
}
```

**JavaScript**

``` syntax
var iter = Windows.ApplicationModel.Background.BackgroundTaskRegistration.allTasks.first();
var hascur = iter.hasCurrent;
while (hascur) {
    var cur = iter.current.value;
    if (cur.name === “MobileOperatorNotificationHandler”) {
        cur.addEventListener("progress", new ProgressHandler(cur).onProgress);
        cur.addEventListener("completed", new CompleteHandler(cur).onCompleted);
    }
    hascur = iter.moveNext();
}

//
// Handle background task progress.
//
function ProgressHandler(task) {
    this.onProgress = function (args) {
       try {
           var progress = "Progress: " + args.progress + "%";
       } catch (ex) {
           displayError(ex);
       }
   };
}

//
// Handle background task completion.
//
function CompleteHandler(task) {
    this.onCompleted = function (args) {
        try {
            var key = task.taskId;
        } catch (ex) {
            displayError(ex);
        }
    };
}
```

## <a name="span-idtsspanspan-idtsspantroubleshooting"></a><span id="ts"></span><span id="TS"></span>故障排除


使用这些部分可帮助解决可能出现的问题。

### <a name="span-idtrigger_metadata_parsing_to_register_background_tasksspanspan-idtrigger_metadata_parsing_to_register_background_tasksspanspan-idtrigger_metadata_parsing_to_register_background_tasksspantrigger-metadata-parsing-to-register-background-tasks"></a><span id="Trigger_metadata_parsing_to_register_background_tasks"></span><span id="trigger_metadata_parsing_to_register_background_tasks"></span><span id="TRIGGER_METADATA_PARSING_TO_REGISTER_BACKGROUND_TASKS"></span>触发元数据分析以注册后台任务

对于用户，如果连接了移动宽带设备，Windows 8、Windows 8.1 和 Windows 10 会自动安装移动宽带应用和关联的服务元数据，并注册在服务元数据中定义的后台任务。 但是，在 Windows 8.1 中，应用程序不会自动固定到 "开始" 屏幕。

开发人员可以通过按**F5**键 (或右键单击并在桌面上的 "**设备和打印机**" 窗口中选择 "**刷新**) ，手动触发 windows 8、Windows 8.1 和 windows 10 来分析服务元数据并注册后台任务。 仅当部署了应用时，通过服务元数据分析的后台任务注册才会成功。

### <a name="span-idverify_that_background_tasks_are_correctly_registered_spanspan-idverify_that_background_tasks_are_correctly_registered_spanspan-idverify_that_background_tasks_are_correctly_registered_spanverify-that-background-tasks-are-correctly-registered"></a><span id="Verify_that_background_tasks_are_correctly_registered_"></span><span id="verify_that_background_tasks_are_correctly_registered_"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_CORRECTLY_REGISTERED_"></span>验证是否正确注册了后台任务

开发人员可以通过查看 **应用程序和服务日志 \\ Microsoft \\ Windows \\ DeviceSetupManager**下的事件日志来验证 (DSM) 是否已正确分析了服务元数据。

1.  打开事件查看器。

2.  在 " **菜单** " 选项卡上，选择 " **视图**"，然后单击 " **显示分析和调试日志**"。

3.  浏览到 **应用程序和服务日志 \\ Microsoft \\ Windows \\ DeviceSetupManager**。

相关事件包括事件 ID 220，该事件 ID 为，指示 DSM 已成功为 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件注册了后台任务，事件 id 7900 指示了在元数据包中发现的任何错误。

### <a name="span-idverify_that_provisioning_metadata_is_successfully_appliedspanspan-idverify_that_provisioning_metadata_is_successfully_appliedspanspan-idverify_that_provisioning_metadata_is_successfully_appliedspanverify-that-provisioning-metadata-is-successfully-applied"></a><span id="Verify_that_provisioning_metadata_is_successfully_applied"></span><span id="verify_that_provisioning_metadata_is_successfully_applied"></span><span id="VERIFY_THAT_PROVISIONING_METADATA_IS_SUCCESSFULLY_APPLIED"></span>验证是否已成功应用设置元数据

应用预配元数据时，验证 [**ProvisionFromXmlDocumentResults. AllElementsProvisioned**](/uwp/api/Windows.Networking.NetworkOperators.ProvisionFromXmlDocumentResults#Windows_Networking_NetworkOperators_ProvisionFromXmlDocumentResults_AllElementsProvisioned) 是否为 true。 如果没有，请检查 ProvisionResultsXml 以获取有关错误的更多详细信息。 常见的移动宽带错误包括：

-   PC 和预配文件 (配置文件中的 SIM 不匹配， \_ \_) 中找不到错误。

-   预配文件中的 CarrierId 与体验元数据中的服务号不匹配。

### <a name="span-idverify_that_background_tasks_are_being_run_by_the_system_event_brokerspanspan-idverify_that_background_tasks_are_being_run_by_the_system_event_brokerspanspan-idverify_that_background_tasks_are_being_run_by_the_system_event_brokerspanverify-that-background-tasks-are-being-run-by-the-system-event-broker"></a><span id="Verify_that_background_tasks_are_being_run_by_the_System_Event_Broker"></span><span id="verify_that_background_tasks_are_being_run_by_the_system_event_broker"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_BEING_RUN_BY_THE_SYSTEM_EVENT_BROKER"></span>验证系统事件代理是否正在运行后台任务

可以通过检查事件查看器来验证 Windows 是否正在生成 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件，以及事件代理是否正在运行应用的后台任务。 这些事件的日志记录在默认情况下是关闭的，可以通过执行以下步骤来启用：

1.  打开事件查看器。

2.  在 " **菜单** " 选项卡上，选择 " **视图**"，然后单击 " **显示分析和调试日志**"。

3.  浏览到 **应用程序和服务日志 \\ Microsoft \\ Windows \\ BackgroundTaskInfrastructure**。

4.  右键单击 " **诊断日志** "，然后选择 " **启用日志**"。

启用日志后，成功执行后台任务会导致事件**ID = 1**的事件，该事件具有以下描述： "具有入口点 &lt; 后台 \_ 任务 \_ 命名空间 \_ 名称的 &gt; 后台任务实例。 &lt;\_ \_ \_ &gt; 已在会话1中创建了后台任务类名称和名称 MobileOperatorNotificationHandler，并给定了 ID {11111111-1111-1111-1111-111111111111} "。

如果未运行后台任务，请首先验证服务元数据中指定的后台任务的名称是否与包的 AppXManifest.xml 文件中的名称匹配。 验证在部署应用程序后，将触发分析服务元数据并插入移动宽带设备。

### <a name="span-idverify_that_windows_receives_sms_and_ussd_notificationsspanspan-idverify_that_windows_receives_sms_and_ussd_notificationsspanspan-idverify_that_windows_receives_sms_and_ussd_notificationsspanverify-that-windows-receives-sms-and-ussd-notifications"></a><span id="Verify_that_Windows_receives_SMS_and_USSD_notifications"></span><span id="verify_that_windows_receives_sms_and_ussd_notifications"></span><span id="VERIFY_THAT_WINDOWS_RECEIVES_SMS_AND_USSD_NOTIFICATIONS"></span>验证 Windows 是否收到短信和 USSD 通知

可以通过在事件查看器中检查 SmsRouter 事件来验证 Windows 是否正在接收短信和 USSD 通知。

在事件查看器中，在 " **应用程序和服务日志" 下， \\ microsoft \\ Windows \\ Mobile-宽带-smsrouter-smsrouter \\ microsoft-** smsrouter，是诸如 "smsrouter 接收到 SMS 操作员通知消息" 和 "smsrouter 收到短信" 之类的条目。 在 **应用程序和服务日志下， \\ Microsoft \\ Windows \\ Mobile-宽带-SmsApi \\ SmsApi** 是一些条目，例如 "App： SDKSamples SmsSendReceive 在移动宽带设备上发送短信： {11111111-1111-1111-1111-111111111111} "。

### <a name="span-idreceived_sms_messages_are_not_detected_as_operator_notificationsspanspan-idreceived_sms_messages_are_not_detected_as_operator_notificationsspanspan-idreceived_sms_messages_are_not_detected_as_operator_notificationsspanreceived-sms-messages-are-not-detected-as-operator-notifications"></a><span id="Received_SMS_messages_are_not_detected_as_operator_notifications"></span><span id="received_sms_messages_are_not_detected_as_operator_notifications"></span><span id="RECEIVED_SMS_MESSAGES_ARE_NOT_DETECTED_AS_OPERATOR_NOTIFICATIONS"></span>未检测到收到的短信消息作为操作员通知

如果未检测到接收到的 SMS 作为操作员通知，请在帐户设置元数据中验证管理短信通知的自定义筛选规则。 有关设置元数据的详细信息，请参阅 [帐户预配](account-provisioning.md)。

特别是，如果帐户预配元数据指定了发送方电话号码，则验证指定的数字格式是否与使用 SMS Api 接收的消息中的格式匹配。 若要验证此是否正确匹配，请暂时将模式更改为 **\[^\]\\** *，以匹配来自此发件人的所有消息。

## <a name="span-idsampspanspan-idsampspansample-backgroundtaskjs-file"></a><span id="samp"></span><span id="SAMP"></span>示例 backgroundtask.js 文件


``` syntax
//
// A JavaScript background task runs a specified JavaScript file.
//
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,
        networkOperatorEventType = Windows.Networking.NetworkOperators.NetworkOperatorEventMessageType,
        key = null,
        settings = Windows.Storage.ApplicationData.current.localSettings;

    try {       
        var details = backgroundTaskInstance.triggerDetails;

        switch (details.notificationType) {
            case networkOperatorEventType.gsm:
                var textMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(details.smsMessage);
                showToast("Gsm Msg From: " + textMessage.from + "; TimeStamp: " + textMessage.timestamp, details.message);
                
                break;
            case networkOperatorEventType.cdma:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.ussd:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.dataPlanThresholdReached:
                showToast("Mobile Broadband message", "Data plan threshold reached");
                break;
            case networkOperatorEventType.dataPlanReset:
                showToast("Mobile Broadband message", "Data plan reset");
                break;
            case networkOperatorEventType.dataPlanDeleted:
                showToast("Mobile Broadband message", "Data plan deleted");
                break;
            case networkOperatorEventType.profileConnected:
                showToast("Mobile Broadband message", "Profile connected");
                break;
            case networkOperatorEventType.profileDisconnected:
                showToast("Mobile Broadband message", "Profile disconnected");
                break;
            case networkOperatorEventType.registeredRoaming:
                showToast("Mobile Broadband message", "Registered roaming");
                break;
            case networkOperatorEventType.registeredHome:
                showToast("Mobile Broadband message", "Registered home");
                break;
            case networkOperatorEventType.tetheringEntitlementCheck:
                showToast("Mobile Broadband message", "Entitlement check completed");
                break;
            default:
                showToast("Mobile Broadband message", "Unknown message");
                break;
        }
        taskSucceeded();
    }
    catch (exception) {
        taskFailed();
    }

    function showToast(title, body) {

        var notifications = Windows.UI.Notifications;
        var toastNotificationManager = Windows.UI.Notifications.ToastNotificationManager;
        var toastXml = toastNotificationManager.getTemplateContent(notifications.ToastTemplateType.toastText02);

        //
        // Pass to app through eventArguments.arguments.
        //
        var temp = "\"Title\"" + ":" + "\"" + title + "\"" + "," + "\"Message\"" + ":" + "\"" + body + "\"";
        if (temp.length > 251) {
            temp = temp.substring(0, 251);
        }
        toastXml.selectSingleNode("/toast").setAttribute("launch", "'{" + temp + "}'");

        var textNodes = toastXml.getElementsByTagName("text");
        textNodes[0].appendChild(toastXml.createTextNode(title));
        textNodes[1].appendChild(toastXml.createTextNode(body));

        var toast = new notifications.ToastNotification(toastXml);
        toastNotificationManager.createToastNotifier().show(toast);        
    }

    //
    // This function is called when the background task is completed successfully.
    //
    function taskSucceeded() {
        //
        // Use the succeeded property to indicate that this background task completed successfully.
        //
        backgroundTaskInstance.succeeded = true;
        backgroundTask.taskInstance.progress = 100;
        console.log("Background " + backgroundTask.taskInstance.task.name + " Completed");

        //
        // Write to localSettings to indicate that this background task completed.
        //
        key = backgroundTaskInstance.task.taskId.toString();
        settings.values[key] = "Completed";

        //
        // A JavaScript background task must call close when it is done.
        //
        close();
    }

    //
    // If the task was canceled or failed, stop the background task.
    //
    function taskFailed() {
        console.log("Background " + backgroundTask.taskInstance.task.name + " Failed");
        backgroundTaskInstance.succeeded = false;

        key = backgroundTaskInstance.task.taskId.toString();
        settings.values[key] = "Failed";

        close();
    }
})();
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)

 

