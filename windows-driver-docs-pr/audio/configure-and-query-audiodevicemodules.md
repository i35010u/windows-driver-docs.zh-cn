---
description: 本文介绍如何从音频设备模块发送命令和接收更改通知。 从通用 Windows 平台 (UWP) 应用。
ms.assetid: AA053196-F331-4CBE-B032-4E9CBEAC699C
title: 配置和查询音频设备模块
label: Configure and query audio device modules
template: ''
ms.author: drewbat
ms.date: 06/28/2017
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b15d9b53aff86862b3216f7232404b1a1cf26721
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208211"
---
# <a name="configure-and-query-audio-device-modules"></a>配置和查询音频设备模块 

本文介绍如何从 UWP 应用发送命令和接收来自音频设备模块的更改通知。 音频设备模块可以是硬件效果处理单元或音频驱动程序定义的任何其他音频配置模块。 此功能旨在使模块提供程序能够创建 UWP 应用，这些应用允许用户控制和获取 DSP 中运行的音频处理模块的状态信息。 若要使用本文中所示的音频设备模块 Api，必须在应用包清单中指定受限的 *audioDeviceConfiguration* 功能。

## <a name="get-an-instance-of-the-audiodevicemodulesmanager-class"></a>获取 AudioDeviceModulesManager 类的实例
本文中所示的所有音频设备模块操作都首先获取 **[AudioDeviceModulesManager](/uwp/api/windows.media.devices.audiodevicemodulesmanager)** 的实例。 首先调用**[MediaDevice](/uwp/api/windows.media.devices.mediadevice)** 类的静态**[GetDefaultAudioRenderId](/uwp/api/windows.media.devices.mediadevice.getdefaultaudiorenderid)** 方法来执行此操作。 这会返回默认音频呈现设备的 ID，该 ID 随后会传递到 **AudioDeviceModulesManager** 的构造函数中，以创建与音频设备关联的类的实例。

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
```

## <a name="query-for-installed-audio-device-modules"></a>查询安装的音频设备模块

通过调用**[AudioDeviceModulesManager](/uwp/api/windows.media.devices.audiodevicemodulesmanager)** 类的**[FindAll](/uwp/api/windows.media.devices.audiodevicemodulesmanager.findall)** ，查询所有已安装的音频设备模块。 通过调用 **[FindAllById](/uwp/api/windows.media.devices.audiodevicemodulesmanager.findallbyid)** 并传入请求的模块的 ID，查询特定的一组音频设备模块。 下面的示例定义一组模块的 ID，调用 **FindAllById** 来检索 **[AudioDeviceModule](/uwp/api/windows.media.devices.audiodevicemodule)** 对象的列表，然后将每个模块的详细信息输出到调试输出。

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
## <a name="send-a-command-to-an-audio-device-module-and-receive-result-data"></a>向音频设备模块发送命令并接收结果数据
通过对**[AudioDeviceModule](/uwp/api/windows.media.devices.audiodevicemodule)** 对象调用**[SendCommandAsync](/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** ，将命令发送到音频设备模块。 **SendCommandAsync**方法采用字节数组作为参数。 通常，此字节数组包含一个命令标识符，后跟与命令相关联的数据，但命令格式和值完全由供应商定义，并被系统视为透明。

**SendCommandAsync**方法返回一个异步操作，该操作在完成后返回表示命令结果的**[ModuleCommandResult](/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** 对象。 **[Status](/uwp/api/windows.media.devices.modulecommandresult.status)** 属性包含一个枚举值，该值指示系统是否可以执行该命令。 这并不一定表示音频设备模块已成功执行命令。 **[Result](/uwp/api/windows.media.devices.modulecommandresult.result)** 属性包含一个字节数组，该数组由音频设备模块返回，用于指示命令的状态。 通常，这将是一个值，指示成功或失败后跟命令的数据结果。 与模块命令一样，模块响应格式和值都是由供应商定义的。

下面的示例调用 **FindAllAsync** 来检索一组音频设备模块。 **[DataWriter](/uwp/api/windows.storage.streams.datawriter)** 用于创建包含示例命令和数据的字节数组。 调用**SendCommandAsync**以发送命令缓冲区，并在异步操作完成后返回**ModuleCommandResult** 。 如果命令执行成功，则首先使用 **[DataReader](/uwp/api/windows.storage.streams.datareader)** 来读取从模块返回的整数状态值。 如果此值是供应商定义的成功值，则将读取并使用应用程序（如）更新 UI。


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

## <a name="receive-notifications-when-audio-device-modules-are-modified"></a>修改音频设备模块时接收通知
通过注册 **[ModuleNotificationReceived](/uwp/api/windows.media.devices.audiodevicemodulesmanager.modulenotificationreceived)** 事件来更新音频设备模块后，应用可以接收通知。 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);

audioModuleManager.ModuleNotificationReceived += AudioModuleManager_ModuleNotificationReceived;
``` 

当修改与当前音频设备关联的任何音频设备模块时，将引发**ModuleNotificationReceived** 。 若要确定事件是否与特定模块关联，请通过访问传递到事件处理程序中的**[AudioDeviceModuleNoticiationEventArgs](/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs)** 的**[module](/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.module)** 属性，然后检查标识该模块的**[ClassId](/uwp/api/windows.media.devices.audiodevicemodule.classid)** 属性来获取**AudioDeviceModule**的实例。 与事件关联的数据将作为存储在事件参数的 **[NotificationData](/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.notificationdata)** 属性中的字节数组传递。 与命令和结果一样，返回的字节数组的格式为供应商定义的格式。 在以下示例中，如果通知数据的第一个字节包含模块的 "回响级别" 设置的示例值，则将读取并使用该数据来更新 UI。

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