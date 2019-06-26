---
title: 开发用于处理 MobileOperatorNotification 事件的应用
description: 开发用于处理 MobileOperatorNotification 事件的应用
ms.assetid: 3c483888-8ec4-4270-af3e-ef1efc995171
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da84f8dbc982eb1a011e75e16c1a1867fa969b7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381507"
---
# <a name="develop-an-app-to-handle-the-mobileoperatornotification-event"></a>开发用于处理 MobileOperatorNotification 事件的应用


本主题说明如何开发移动宽带应用程序处理[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。

-   [最佳做法](#bp)

-   [步骤 1：后台任务协定声明](#stepone)

-   [步骤 2：后台任务处理程序](#steptwo)

-   [步骤 3：处理激活事件](#stepthree)

-   [步骤 4：处理后台任务完成处理程序](#stepfour)

-   [疑难解答](#ts)

-   [示例 backgroundtask.js 文件](#samp)

## <a name="span-idbpspanspan-idbpspanbest-practices"></a><span id="bp"></span><span id="BP"></span>最佳做法


对于后台事件处理，应使用以下最佳实践：

-   不注册的后台事件不能对其执行操作。 处理这些事件将不必要地占用应用配额。

-   不要在后台事件收到执行大量的处理。

-   请考虑将延迟到下一次处理应用程序启动。

-   请考虑显示 toast 通知和更新磁贴对背景事件作出响应。 移动宽带应用可以处理后台事件有效负载。

后台任务的详细信息，请参阅[后台任务简介](https://go.microsoft.com/fwlink/p/?linkid=313924)。

## <a name="span-idsteponespanspan-idsteponespanstep-1-background-task-contract-declaration"></a><span id="stepone"></span><span id="STEPONE"></span>步骤 1:后台任务协定声明


为识别由移动宽带应用提供的后台任务体验的 Windows，应用必须声明提供对系统功能的扩展。

若要在 Visual Studio 项目的 package.appxmanifest 文件中进行声明，执行以下步骤：

**若要声明的后台任务协定**

1.  在中**解决方案资源管理器**，双击你的项目的 package.appxmanifest 文件。

2.  上**声明**选项卡上，从**可用声明**，选择**后台任务**，然后单击**添加**。

3.  下**属性**标题下方，输入以下应用信息：

    -   在中**起始页**框下**应用设置**，为移动宽带应用使用 JavaScript 和 HTML，输入处理的应用中的后台任务的文件名称 (例如， **backgroundtask.js**)。

    -   下**支持的任务类型**标题下方，单击**系统事件**复选框。

如果操作无误，您应类似于以下的扩展元素 package.appxmanifest 文件中。

``` syntax
<Extension Category="windows.backgroundTasks" StartPage="backgroundtask.js">
  <BackgroundTasks>
    <Task Type="systemEvent" />
  </BackgroundTasks>
</Extension>
```

## <a name="span-idsteptwospanspan-idsteptwospanstep-2-background-task-handler"></a><span id="steptwo"></span><span id="STEPTWO"></span>步骤 2:后台任务处理程序


如果您的应用程序提供移动运营商通知，声明中，它必须提供后台任务激活的处理程序。 该处理程序将获得移动运营商网络帐户 ID 和事件数据从[ **Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails)。

由于唯一支持的后台任务的 UI **Toast**，后台任务处理程序可以显示 Toast 或保存[ **NetworkOperatorNotificationEventDetails** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails)到本地存储。

下面的代码示例演示了专为运行时收到新管理 SMS 通知的后台任务。

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

### <a name="span-idshowtileandtoastnotificationsspanspan-idshowtileandtoastnotificationsspanspan-idshowtileandtoastnotificationsspanshow-tile-and-toast-notifications"></a><span id="Show_tile_and_toast_notifications"></span><span id="show_tile_and_toast_notifications"></span><span id="SHOW_TILE_AND_TOAST_NOTIFICATIONS"></span>显示磁贴和 toast 通知

我们建议你显示这两个 toast 并在你的移动宽带应用磁贴通知，因为用户可能会遗漏由于暂时性本质的 toast 通知。 适用于 toast 通知和磁贴更新体验的设计指南，请参阅[设计用户体验的移动宽带应用](designing-the-user-experience-of-a-mobile-broadband-app.md)。

**若要启用的 toast 通知**

1.  在中**解决方案资源管理器**，双击你的项目的 package.appxmanifest 文件。

2.  上**应用程序 UI**选项卡上，在**通知**标题时，设置**支持 toast 通知**到**是**。

如果操作无误，您应类似于以下的扩展元素 package.appxmanifest 文件中。

``` syntax
<VisualElements … ToastCapable="true"… />
```

下面的代码演示如何在后台任务句柄中显示一条 toast 通知：

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

### <a name="span-idgetsmstextmessagespanspan-idgetsmstextmessagespanspan-idgetsmstextmessagespanget-sms-text-message"></a><span id="Get_SMS_text_message"></span><span id="get_sms_text_message"></span><span id="GET_SMS_TEXT_MESSAGE"></span>获取短信

如果由传入的 SMS 消息触发后台任务，后台任务详细信息将在其有效负载中附带的 SMS 对象。

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

### <a name="span-iduselocalstoragespanspan-iduselocalstoragespanspan-iduselocalstoragespanuse-local-storage"></a><span id="Use_local_storage"></span><span id="use_local_storage"></span><span id="USE_LOCAL_STORAGE"></span>使用本地存储

后台任务可以使用本地存储来保存从后台事件中，获取消息，以便应用可以使用该信息更高版本。

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

下面的代码演示如何检索存储的应用程序中的后台任务处理程序的消息：

**JavaScript**

``` syntax
var settings = Windows.Storage.ApplicationData.current.localSettings;
    var keyMessage = "BA5857FA-DE2C-4A4A-BEF2-49D8B4130A39";
    var operatorMessage = settings.values[keyMessage];
```

## <a name="span-idstepthreespanspan-idstepthreespanstep-3-handle-the-activation-event"></a><span id="stepthree"></span><span id="STEPTHREE"></span>步骤 3:处理激活事件


如果 toast 设置参数，它将被传递到应用程序通过**detail.arguments**。

在 JavaScript 中或C#，则处理[ **WinJS.Application.onactivated** ](https://docs.microsoft.com/previous-versions/windows/apps/br212679(v=win.10))事件，然后检查传递给事件处理程序的事件参数。 从 toast 激活传递事件参数的类型[ **Windows.UI.WebUI.WebUILaunchActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.WebUI.WebUILaunchActivatedEventArgs)。 如果事件参数的**detail.kind**属性是[ **Windows.ApplicationModel.Activation.ctivationKind**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind)。**启动**，应用程序提供启动体验或通知体验，具体取决于事件参数的**detail.argument**属性设置为**null**.

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

## <a name="span-idstepfourspanspan-idstepfourspanstep-4-handle-background-task-completion-handlers"></a><span id="stepfour"></span><span id="STEPFOUR"></span>步骤 4:处理后台任务完成处理程序


前台应用程序还可以注册完成处理程序的后台任务完成时收到通知。 完成状态或在发生任何异常**运行**的后台任务的方法传递到完成处理程序在前台应用程序中。 如果应用挂起的任务完成时，它接收完成通知恢复应用程序的下一次。 如果应用已处于**Terminated**状态中时，它不接收完成通知。 如果后台任务需要保留已成功运行的信息，它必须通过使用状态管理器或另一种方法，例如当它返回到该应用可以读取文件中保存信息**运行**状态。

**重要**  尽管移动运营商后台事件已由应用到系统自动注册，但应用仍需要运行至少一次，以注册到后台完成或正在进行处理。

 

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


使用这些部分来帮助解决可能出现的问题。

### <a name="span-idtriggermetadataparsingtoregisterbackgroundtasksspanspan-idtriggermetadataparsingtoregisterbackgroundtasksspanspan-idtriggermetadataparsingtoregisterbackgroundtasksspantrigger-metadata-parsing-to-register-background-tasks"></a><span id="Trigger_metadata_parsing_to_register_background_tasks"></span><span id="trigger_metadata_parsing_to_register_background_tasks"></span><span id="TRIGGER_METADATA_PARSING_TO_REGISTER_BACKGROUND_TASKS"></span>触发器元数据分析注册后台任务

对于用户，当连接移动宽带设备，Windows 8、 Windows 8.1 和 Windows 10 自动安装的移动宽带应用和关联的服务元数据和寄存器的后台任务的服务元数据中定义的。 但是，在 Windows 8.1 应用程序不会自动固定到开始屏幕。

分析服务元数据并通过按注册后台任务的 Windows 8、 Windows 8.1 和 Windows 10 开发人员可以手动触发**F5**密钥 (或右键单击并选择**刷新**) 在**设备和打印机**窗口在桌面上。 通过分析的服务元数据的后台任务注册成功仅当应用程序部署。

### <a name="span-idverifythatbackgroundtasksarecorrectlyregisteredspanspan-idverifythatbackgroundtasksarecorrectlyregisteredspanspan-idverifythatbackgroundtasksarecorrectlyregisteredspanverify-that-background-tasks-are-correctly-registered"></a><span id="Verify_that_background_tasks_are_correctly_registered_"></span><span id="verify_that_background_tasks_are_correctly_registered_"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_CORRECTLY_REGISTERED_"></span>验证正确注册后台任务

开发人员可以验证设备安装程序管理器 (DSM) 正确具有通过查看下的事件日志分析服务元数据**应用程序和服务日志\\Microsoft\\Windows\\DeviceSetupManager**。

1.  打开事件查看器。

2.  上**菜单**选项卡上，选择**视图**，然后单击**显示分析和调试日志**。

3.  浏览到**应用程序和服务日志\\Microsoft\\Windows\\DeviceSetupManager**。

感兴趣的事件包括事件 ID 为 220，该值指示 DSM 已成功注册的后台任务[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件，以及指示元数据中找到的任何错误的事件 ID 7900包。

### <a name="span-idverifythatprovisioningmetadataissuccessfullyappliedspanspan-idverifythatprovisioningmetadataissuccessfullyappliedspanspan-idverifythatprovisioningmetadataissuccessfullyappliedspanverify-that-provisioning-metadata-is-successfully-applied"></a><span id="Verify_that_provisioning_metadata_is_successfully_applied"></span><span id="verify_that_provisioning_metadata_is_successfully_applied"></span><span id="VERIFY_THAT_PROVISIONING_METADATA_IS_SUCCESSFULLY_APPLIED"></span>验证已成功应用预配的元数据

当应用预配的元数据，验证是否[ **ProvisionFromXmlDocumentResults.AllElementsProvisioned** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisionFromXmlDocumentResults#Windows_Networking_NetworkOperators_ProvisionFromXmlDocumentResults_AllElementsProvisioned)为 true。 如果没有，检查有关错误的更多详细信息的 ProvisionResultsXml。 常见的移动宽带错误包括：

-   在 PC 中的 SIM 和预配文件之间不匹配 (配置文件失败，出现错误\_不\_找到)。

-   预配文件中的 CarrierId 和体验元数据中的服务数字之间不匹配。

### <a name="span-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanspan-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanspan-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanverify-that-background-tasks-are-being-run-by-the-system-event-broker"></a><span id="Verify_that_background_tasks_are_being_run_by_the_System_Event_Broker"></span><span id="verify_that_background_tasks_are_being_run_by_the_system_event_broker"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_BEING_RUN_BY_THE_SYSTEM_EVENT_BROKER"></span>验证系统事件代理正在运行后台任务

你可以验证 Windows 是否正在生成[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件和事件代理由通过检查事件查看器，运行应用的后台任务。 这些事件的日志记录默认处于关闭状态，并且可以启用通过执行以下步骤：

1.  打开事件查看器。

2.  上**菜单**选项卡上，选择**视图**，然后单击**显示分析和调试日志**。

3.  浏览到**应用程序和服务日志\\Microsoft\\Windows\\BackgroundTaskInfrastructure**。

4.  右键单击**诊断日志**，然后选择**启用日志**。

成功执行的后台任务启用日志后，生成的事件**事件 ID = 1**具有以下说明："后台任务的入口点的实例&lt;背景\_任务\_命名空间\_名称&gt;。&lt;背景\_任务\_类\_名称&gt;，并且已在会话 1 中创建和给定的 ID 名称 MobileOperatorNotificationHandler {11111111-1111-1111-1111-111111111111}。"

如果不运行后台任务时，首先验证后台任务在服务元数据中指定的名称与您的包的 AppXManifest.xml 文件中的名称匹配。 验证后部署该应用程序，分析服务元数据将触发并插入移动宽带设备。

### <a name="span-idverifythatwindowsreceivessmsandussdnotificationsspanspan-idverifythatwindowsreceivessmsandussdnotificationsspanspan-idverifythatwindowsreceivessmsandussdnotificationsspanverify-that-windows-receives-sms-and-ussd-notifications"></a><span id="Verify_that_Windows_receives_SMS_and_USSD_notifications"></span><span id="verify_that_windows_receives_sms_and_ussd_notifications"></span><span id="VERIFY_THAT_WINDOWS_RECEIVES_SMS_AND_USSD_NOTIFICATIONS"></span>验证 Windows 接收短信和 USSD 通知

你可以验证 Windows 通过检查事件查看器中的 SmsRouter 事件接收短信和 USSD 的通知。

在事件查看器下**应用程序和服务日志\\Microsoft\\Windows\\移动宽带体验 SmsRouter\\Microsoft Windows SMSRouter**，条目如"SMSRouter 收到短信运算符通知消息"和"SMSRouter 收到短信"。 下**应用程序和服务日志\\Microsoft\\Windows\\移动宽带体验 SmsApi\\SMSApi**有条目，例如"应用程序：Microsoft.SDKSamples.SmsSendReceive 上移动宽带设备发送短信： {11111111-1111-1111-1111-111111111111}"。

### <a name="span-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanspan-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanspan-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanreceived-sms-messages-are-not-detected-as-operator-notifications"></a><span id="Received_SMS_messages_are_not_detected_as_operator_notifications"></span><span id="received_sms_messages_are_not_detected_as_operator_notifications"></span><span id="RECEIVED_SMS_MESSAGES_ARE_NOT_DETECTED_AS_OPERATOR_NOTIFICATIONS"></span>接收的 SMS 消息不被检测为运营商通知

如果收到的短信被检测为不运营商通知，请验证管理帐户预配的元数据中的短信通知的自定义筛选规则。 有关预配的元数据的详细信息，请参阅[帐户预配](account-provisioning.md)。

具体而言，如果帐户预配的元数据指定发件人的电话号码，验证的数字格式指定与匹配的接收的消息中通过使用 SMS Api。 若要验证这正确匹配，暂时更改到的模式 **\[ ^ \] \\** * 来匹配来自该发件人的所有消息。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)

 

 






