---
Description: This article shows how to send commands and receive change notifications from audio device modules. from a Universal Windows Platform (UWP) app.
ms.assetid: AA053196-F331-4CBE-B032-4E9CBEAC699C
title: 配置和查询音频设备模块
label: Configure and query audio device modules
template: ''
ms.author: drewbat
ms.date: 06/28/2017
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 608926ac8c1eab801eecb31027c9261e4041134a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520573"
---
# <a name="configure-and-query-audio-device-modules"></a>配置和查询音频设备模块 

本文介绍如何将命令发送和接收来自音频设备模块从 UWP 应用的更改通知。 音频设备模块可能处理单元或定义的音频驱动程序的任何其他音频配置模块的硬件效果。 此功能旨在启用模块提供程序，以创建允许用户控制，并从运行在 DSP 中的音频处理模块获取状态信息的 UWP 应用。 若要使用的音频设备模块这篇文章中所示的 Api，必须指定的受限*audioDeviceConfiguration*应用包清单中的功能。

## <a name="get-an-instance-of-the-audiodevicemodulesmanager-class"></a>获取 AudioDeviceModulesManager 类的实例
在本文中所示的所有音频设备模块操作开始通过获取的实例 **[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)**。 执行此操作通过第一个调用静态**[GetDefaultAudioRenderId](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice.getdefaultaudiorenderid)** 方法**[MediaDevice](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice)** 类。 这将返回默认音频渲染设备，然后传递到构造函数的 ID **AudioDeviceModulesManager**创建与音频设备相关联的类的实例。

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
```

## <a name="query-for-installed-audio-device-modules"></a>已安装的音频设备模块的查询

查询对所有通过调用已安装的音频设备模块**[FindAll](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.findall)** 的**[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)** 类。 查询的一组特定的音频设备模块通过调用**[FindAllById](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.findallbyid)** 并传入请求的模块的 ID。 下面的示例定义一个 ID 为一组模块，调用**FindAllById**若要检索的列表**[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** 对象，并输出每个详细信息，然后到调试输出的模块。

C#
```csharp
public const string Contoso_AudioDeviceModuleId = "F72E09C3-FEBA-4C50-93BE-2CA56123AF09";
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var classId = module.ClassId;
    var name = module.DisplayName;
    var minorVersion = module.MinorVersion;
    var majorVersion = module.MajorVersion;
    var instanceId = module.InstanceId;

        Debug.WriteLine($"{classId} : {name} : {minorVersion} : {majorVersion} : {instanceId}");
}
``` 
## <a name="send-a-command-to-an-audio-device-module-and-receive-result-data"></a>将命令发送到音频设备模块和接收结果数据
将命令发送到一个音频设备模块，通过调用**[SendCommandAsync](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** 上**[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** 对象。 **SendCommandAsync**方法采用字节数组作为参数。 此字节数组通常包含后跟与命令关联的数据的命令标识符，但命令格式和值是完全供应商定义的由系统被视为透明。

**SendCommandAsync**方法返回的异步操作，完成后，返回**[ModuleCommandResult](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** 对象，表示的结果命令。 **[状态](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult.status)** 属性包含一个枚举值，指示系统是否能够执行命令。 这并不一定表示音频设备模块已能够成功执行该命令。 **[结果](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult.result)** 属性包含一个字节数组，返回的音频设备模块，以指示该命令的状态。 通常情况下，这将是一个值，指示成功或失败后跟命令的数据结果。 与模块命令一样，模块响应格式和值是供应商定义。

下面的示例调用**FindAllAsync**检索一组音频设备模块。 一个**[DataWriter](https://docs.microsoft.com/uwp/api/windows.storage.streams.datawriter)** 用于创建包含示例命令和数据的字节数组。 **SendCommandAsync**调用来发送命令缓冲区和异步操作完成之后, **ModuleCommandResult**返回。 如果命令执行成功， **[DataReader](https://docs.microsoft.com/uwp/api/windows.storage.streams.datareader)** 首次用于读取从模块返回一个整数状态。 如果此值是供应商定义的成功值，其余的结果数据读取，并使用应用程序中，如更新 UI。


C#
```csharp
public const byte Contoso_ReverbLevel_Command = 30; 
public const byte Contoso_SendCommand_Success = 99;
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var writer = new Windows.Storage.Streams.DataWriter();
    writer.WriteByte(Contoso_ReverbLevel_Command);
    writer.WriteByte(100);

    var command = writer.DetachBuffer();

    var result = await module.SendCommandAsync(command);

    if (result.Status == SendCommandStatus.Success)
    {
        using (DataReader reader = DataReader.FromBuffer(result.Result))
        {
            int bufferStatus = reader.ReadInt32();
            if (bufferStatus == Contoso_SendCommand_Success)
            {
                byte[] data = { 0, 0 };
                reader.ReadBytes(data);
                // Do something with returned data, such as update UI
            }
        }
    }
}
```

## <a name="receive-notifications-when-audio-device-modules-are-modified"></a>音频设备模块进行修改时接收通知
音频设备模块已更新由注册时，应用可以接收通知**[ModuleNotificationReceived](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.modulenotificationreceived)** 事件。 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);

audioModuleManager.ModuleNotificationReceived += AudioModuleManager_ModuleNotificationReceived;
``` 

**ModuleNotificationReceived**将修改与当前的音频设备相关联的任何音频设备模块时引发。 若要确定事件是否与特定模块相关联，请获取的实例**AudioDeviceModule**通过访问**[模块](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.module)** 属性**[AudioDeviceModuleNoticiationEventArgs](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs)** 传递到事件处理程序，然后检查**[ClassId](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.classid)** 属性，标识的模块。 与事件关联的数据进行传递的字节数组中存储**[NotificationData](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.notificationdata)** 事件参数的属性。 与命令和结果，返回的字节数组的格式是供应商定义的。 在下面的示例中，如果通知数据的第一个字节包含模块的混响级别设置的示例值是读取数据，用来更新 UI。

C#
```csharp
public const byte Contoso_ReverbLevel_Data = 25;
```

C#
```csharp
private void AudioModuleManager_ModuleNotificationReceived(AudioDeviceModulesManager sender, AudioDeviceModuleNotificationEventArgs args)
{
    if (args.Module.ClassId == Contoso_AudioDeviceModuleId)
    {
        // Get the coefficient data from the reverb module.
        using (DataReader reader = DataReader.FromBuffer(args.NotificationData))
        {
            // read notification data.
            byte item = reader.ReadByte();

            // if reverb coefficient data are changed.
            if (item == Contoso_ReverbLevel_Data)
            {
                // read the new value
                byte[] data = { 0 };
                reader.ReadBytes(data);
                ReverbLevelSlider.Value = data[0];
            }
        }
    }
}
```
