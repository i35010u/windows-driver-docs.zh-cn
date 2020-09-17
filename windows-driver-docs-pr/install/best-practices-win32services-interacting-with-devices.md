---
title: Win32 服务与设备交互
description: Win32 服务与设备交互
ms.assetid: 0ecc6979-25b3-41eb-8d6f-9eee3b80a56f
ms.date: 03/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1afb05d9612a6b0439e1cfcdcf973cd574ee34e4
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717550"
---
# <a name="win32-services-interacting-with-devices"></a>Win32 服务与设备交互

## <a name="motivation"></a>推动

通过 [INF AddService](./inf-addservice-directive.md) 安装的理想 Win32 服务与设备进行交互的行为类似于 *驱动程序* 与 *设备*交互的方式。  将加载并卸载驱动程序，具体取决于设备是否存在，与设备交互的 Win32 服务应遵循与设备的状态相同的 **启动** 和 **停止** 模式。  

仅当关联设备不再存在时，服务才会启动，以便交互和停止。  此设计模式可确保最大程度地减少不需要的和未定义的行为。  我们将逐步介绍如何将服务设计为遵循此模式。

## <a name="service-install"></a>服务安装

若要安装服务，请使用 [INF AddService](./inf-addservice-directive.md) 指令。  这将允许您创建和启动该服务。

添加使服务按需启动的标志。  这可以通过设置 **StartType = 0x3** 来完成，这会使服务触发器启动。

本部分中的最后一步是使用 **AddTrigger** 指令，使服务在设备接口到达时启动 (参阅 [AddService](./inf-addservice-directive.md) ，了解有关 **AddTrigger**) 的更多详细信息。  下面是如何使用 AddTrigger 的示例：

```
[UserSvc_AddTrigger]
TriggerType = 1                                   ; SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL
Action      = 1                                   ; SERVICE_TRIGGER_ACTION_SERVICE_START
SubType     = %GUID_DEVINTERFACE_OSRFX2%          ; Interface class GUID
DataItem    = 2, "USB\VID_0547&PID_1002"          ; SERVICE_TRIGGER_DATA_TYPE_STRING

[UserSvc_Install]
ServiceType   = 0x10 ; SERVICE_WIN32_OWN_PROCESS
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 0   ; SERVICE_ERROR_IGNORE
ServiceBinary = %13%\oemsvc.exe
AddTrigger    = UserSvc_AddTrigger

```
请注意，在 DataItem 中指定的 HardwareId 是可选的，并且通常仅当使用泛型类接口将触发器的作用域限定为更具体的设备时才需要。  

## <a name="service-runtime"></a>服务运行时
    
从运行时的角度来看，服务的第一步应该是注册设备接口通知。  本页面上提供了有关如何完成此操作的说明性指导： [注册设备接口到达和设备删除的通知](./registering-for-notification-of-device-interface-arrival-and-device-removal.md)。

具体而言，应将 **CM_Register_Notification** 与 **CM_NOTIFY_FILTERY_TYPE_DEVICEINTERFACE** 标志一起使用来完成设备接口通知的相应注册。

>[!NOTE]
>当服务启动时，您无法依赖于您将收到设备接口通知的事实，因为到达通知可能已通过。 相反，您必须获取设备接口列表，以检查是否存在接口。

注册通知后，可以在以下两个步骤中找到所需的设备接口：

1. 从通知回调发现接口
2. 查询现有设备接口的列表，并使用**CM_Get_Device_Interface_List**查找所需的接口

>[!NOTE] 
>请注意，接口可能会在注册通知和查找所需设备接口之间出现。  在这种情况下，接口将在通知回调和接口列表中列出。

找到所需的设备接口后，通过 [CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea)打开该接口的句柄。  

下一步是注册辅助的每个接口的通知，以操作和管理设备。 这可以通过使用 **CM_Register_Notification** 和 **CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE** 标志来完成。  这将确保在设备消失后可以相应地释放句柄。

应跟踪设备接口到达和删除，以便删除上一设备接口意味着可以停止此服务。  删除最后一个接口后，可在此 [页](/windows/desktop/Services/service-servicemain-function) 上) 找到 (详细信息。 可以通过执行以下步骤来完成此操作：

1. 将 **SERVICE_STOP_PENDING** 状态发布到 SCM 以指示服务正在关闭
2. Unitialize/清理服务正在使用的所有内容
3. 将 **SERVICE_STOP** 状态发布到 SCM 完成停止操作

如果正在停止该服务，请确保检查并浏览设备接口的所有现有打开的句柄， (可能没有任何) 并将其清除。 
  
设备接口可以在设备安装期间、设备启用/禁用、设备重新枚举、系统重新启动或未列出的其他方案中返回。  设备接口返回后，将根据其触发器的开始注册来启动该服务。

此流将确保服务在设备接口到达时启动，并在最后一个设备接口不再存在时停止。

## <a name="code-sample--related-links"></a>& 相关链接的代码示例

GitHub 上提供了一个示例，指导服务如何利用这一流事件。  可在以下位置找到该示例： [Win32 服务示例](https://github.com/microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc)。

此外，还可以在[AddService](./inf-addservice-directive.md)页上找到有关**AddTrigger**的有用文档。