---
title: 音频终结点设备的友好名称
description: 音频终结点设备的友好名称
ms.assetid: e0937d20-dd5b-453f-99f6-4e501f0f0e5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e63f8dbdae0d2cb8c6303ff5010da39b322003
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925614"
---
# <a name="friendly-names-for-audio-endpoint-devices"></a>音频终结点设备的友好名称


在 Windows Vista、Windows Server 2008 和更高版本的 Windows 中，音频子系统支持音频终结点设备（例如，发言人、耳机、麦克风和 CD 播放机）的概念。 音频端点的这一概念有助于创建具有用户界面的用户友好音频应用程序，这些用户界面引用用户直接操作的终结点设备。 这些终结点具有友好名称，如 "发言人"、"耳机"、"麦克风" 和 "CD 播放器"，应用程序可以在其用户界面中显示这些名称。 有关终结点设备的详细信息，请参阅[音频终结点设备](https://docs.microsoft.com/windows/win32/coreaudio/audio-endpoint-devices)。

音频子系统将音频适配器上的即插即用（PnP）设备建模为 KS 筛选器。 数据流通过 KS 引脚进入和退出筛选器。 桥接 pin 是一种 KS pin，音频终结点设备通过该 pin 连接到 KS 筛选器。 有关桥接 pin 的详细信息，请参阅[音频筛选器图](audio-filter-graphs.md)。

音频子系统通过检查终结点设备连接到的桥接程序的属性来获取有关音频终结点设备的信息。 一个这样的属性是 " [pin 类别" 属性](pin-category-property.md)（[**\_KSPROPERTY 固定\_类别**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)）。 

对于每个 KS 筛选器，适配器驱动程序都提供了一个表，其中说明了如何在筛选器上描述 KS pin 的属性的[**PCPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)结构。 Pin 类别 GUID 存储在 PCPIN\_描述符结构的**KsPinDescriptor**成员中。 对于网桥，pin 类别 GUID 的值指示连接到桥接 pin 的终结点的类型。 例如，pin 类别 GUID KSNODETYPE\_麦克风指示桥接麦克风连接到麦克风，GUID KSNODETYPE\_扬声器指示桥接到扬声器，依此类推。 KSNODETYPE\_*XXX* guid 在 Ksmedia 头文件中定义。

此外， **PCPIN\_描述符**还包括一个可用于通过唯一名称标识 pin 的 GUID。  此 pin 名称 GUID 存储在 PCPIN\_描述符结构的**KsPinDescriptor.Name**成员中。 此名称 GUID 由（[**\_KSPROPERTY PIN\_名称**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)）属性用来将注册表中找到的友好名称与 PIN 关联起来。 

音频子系统调用**\_KSPROPERTY PIN\_名称**属性，以便将友好名称与音频终结点相关联。 KS 通过首先在描述**KsPinDescriptor.Name** GUID 的注册表中搜索 unicode 字符串来处理此请求。  如果 KS 找不到某个条目，则会在注册表中搜索描述**KsPinDescriptor** GUID 的 unicode 字符串。  

从**Windows 10 REDSTONE 5**开始，搜索注册表时，KS 首先查找设备软件密钥中的条目。  这是由 INF 通过设备驱动程序 INF 的 [模型] 部分引用的 AddReg 部分创建的。  AddReg 部分使用 HKR\\MediaCategories 项来构造这些项。 这样，驱动程序开发人员便可以为名称和类别 Guid 创建特定于设备的友好名称，而不管 GUID 对于设备是否是唯一的。

如果设备的软件密钥中未安装某个条目，或在**Windows 10 REDSTONE 5**之前的操作系统上运行该驱动程序，则 KS 将在\\HKLM 系统\\CurrentControlSet\\Control\\MediaCategories 注册表项下查找。 此第二个键被视为全局命名空间。  从**Windows 10 REDSTONE 5**开始，此空间保留用于全局定义，不应由新驱动程序修改。  在未来的操作系统版本中，将不支持修改此项下的条目。

通过标准类别 Guid 公开 pin 的音频设备应该包含/需要收件箱 KS。INF 或 KSCAPTUR。设备 INF 中的 INF 名称注册。  这些收件箱 Inf 包含驱动程序可能想要填充的预定义类别 Guid 的默认友好名称定义。 这些 Guid 与在 PCPIN\_描述符结构的**KsPinDescriptor**成员中找到的 guid 相同。 例如，类别 GUID KSNODETYPE\_扩音器条目具有关联的友好名称 "麦克风"，类别 guid KSNODETYPE\_发言人条目具有关联的友好名称 "扬声器"，依此类推。

类别和名称 Guid 的 Guid 和友好名称存储在\\HKR MediaCategories 下，而全局定义 HKLM\\SYSTEM\\CurrentControlSet\\Control\\MediaCategories 路径下。 对于注册表中的每个 GUID 名称对，GUID 字符串用作 MediaCategories 键下的子键。  在 GUID 键下，友好名称 "Name" 变量下的 Unicode 字符串值。 

如果音频子系统定义的任何友好名称和 pin 类别都没有充分描述你的设备，你可以定义自己的 pin 类别和名称 Guid，并将友好名称与 INF 中的名称关联。 若要确保你的 pin 类别 GUID 是唯一的，请使用实用程序（如 Uuidgen.exe）生成 GUID。 接下来，修改安装音频适配器的 INF 文件，将 pin 类别 GUID 和友好名称写入注册表路径 HKR\\MediaCategories。 下面的代码示例演示了一个 INF 文件片段，它将两个 pin 类别 Guid 及其关联的友好名称添加到注册表中：

```inf
[Manufacturer]
MyOEMName=Unicorn,NTamd64

[Unicorn.NTamd64]
MyDeviceName=MyDevice,Root\MyDevice

[MyDevice.NT]
Include=ks.inf, kscaptur.inf
Needs=KS.Registration, KSCAPTUR.Registration.NT
CopyFiles=MyDevice.CopyFiles
AddReg=PinNameRegistration

...

[PinNameRegistration]
HKR,%MediaCategories%\%GUID.MyNewEndpointCategory%,Name,,%Name.MyNewEndpointCategory%
HKR,%MediaCategories%\%GUID.MyNewEndpointName%,Name,,%Name.MyNewEndpointName%

...

[Strings]
MyOEMName="Unicorns Inc."
MyDeviceName="Sparkly Unicorn"
MediaCategories="MediaCategories"

GUID.MyNewEndpointCategory="{B72FBD1A-4634-4240-B207-0E6B52F3701C}"
GUID.MyNewEndpoint_2="{71DD3A5D-E303-49A0-ACEE-908634AA9520}"

Name.MyNewEndpointCategory="Unicorn"
Name.MyNewEndpointName="Fred the Unicorn"
```

这两个 GUID 字符串都是由 Uuidgen.exe 生成的。

应用程序可以使用设备的**IPropertyStore**接口访问音频终结点设备的属性。 接口使用在 Functiondiscoverykeys\_Devpkey 和 Mmdeviceapi 头文件中定义的属性键来识别属性。 应用程序可以使用**\_PKEY device\_FriendlyName**属性键检索终结点设备的友好名称。 对于空间受限的用户界面，可以使用**\_PKEY Device\_DeviceDesc**属性键检索较短版本的友好名称。 有关这些属性键的详细信息，请参阅[IMMDevice：： OpenPropertyStore](https://docs.microsoft.com/windows/win32/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore)。

**IPropertyStore**接口实例为音频终结点设备维护持久性属性存储区。 属性存储从与注册表路径 HKLM\\SYSTEM\\\\CurrentControlSet Control\\MediaCategories 中的 KS pin 类别 GUID 关联的友好名称字符串中复制其**PKEY\_Device\_DeviceDesc**属性键的初始值。 应用程序可以从属性存储读取**\_PKEY 设备\_DeviceDesc**属性值（名称字符串），但不能更改值。 但是，用户可以使用 Windows 多媒体控制面板 Mmsys 来修改名称。 例如，在 Windows Vista 中，你可以使用以下步骤来修改呈现终结点设备的名称：

1.  若要运行 Mmsys，请打开命令提示符窗口并输入以下命令：

    ```console
    mmsys.cpl
    ```

    （或者，您也可以通过右键单击通知区域中的扬声器图标，该图标位于任务栏右侧，然后单击 "**播放设备**" 来运行 Mmsys。）

2.  单击呈现设备的名称，然后单击 "**属性**"。

3.  在属性窗口中，单击 "**常规**" 选项卡。友好名称应显示在属性表顶部的文本框中。 你可以编辑该友好名称，然后单击 **"确定"** 保存所做的更改。

上述步骤更改了在音频终结点设备的属性存储中存储的友好名称。 这些步骤不会影响与其他属于相同 KS pin 类别的音频终结点设备关联的友好名称。 它们对可能直接查询 KS 以获取名称的任何组件也不起作用。
