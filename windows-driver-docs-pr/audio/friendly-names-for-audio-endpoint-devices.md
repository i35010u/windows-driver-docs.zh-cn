---
title: 音频终结点设备的友好名称
description: 音频终结点设备的友好名称
ms.assetid: e0937d20-dd5b-453f-99f6-4e501f0f0e5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52fad97a1ada2d3c07f58f67616dcf2d64dfc61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333632"
---
# <a name="friendly-names-for-audio-endpoint-devices"></a>音频终结点设备的友好名称


在 Windows Vista、 Windows Server 2008 和更高版本的 Windows 中，音频子系统支持音频终结点设备，例如，扬声器、 耳机、 麦克风和 CD 播放机的这一概念。 此音频终结点的概念可帮助创建具有用户界面的用户直接操作的终结点设备是指用户友好的音频应用程序。 这些终结点具有如"发言人"、"耳机"、"麦克风"和"CD 播放机"，应用程序可以在其用户界面中显示的友好名称。 有关终结点设备的详细信息，请参阅[音频终结点设备](https://go.microsoft.com/fwlink/p/?linkid=130876)。

音频子系统上的音频适配器作为 KS 筛选器进行建模插 (PnP) 设备。 数据流输入和退出 KS pin 通过筛选器。 桥 pin 是 KS pin 通过其音频终结点设备连接到 KS 筛选器。 有关桥的 pin 的详细信息，请参阅[音频筛选器关系图](audio-filter-graphs.md)。

音频子系统通过检查终结点设备连接到桥固定的属性获取有关音频端点设备的信息。 此类的一个属性是[固定 category 属性](pin-category-property.md)([**KSPROPERTY\_PIN\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff565192))。 

对于每个 KS 筛选器中，适配器驱动程序提供的表[ **PCPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537721)筛选器描述 KS pin 的属性的结构。 GUID 存储在 pin 类别**KsPinDescriptor.Category** PCPIN 成员\_描述符结构。 桥 pin，pin 类别 GUID 表示连接到桥 pin 的终结点的类型。 例如，pin 类别 GUID KSNODETYPE\_麦克风指示桥插针连接到麦克风，GUID KSNODETYPE\_演讲者指示桥插针连接到扬声器，依次类推。 KSNODETYPE\_*XXX* Ksmedia.h 标头文件中定义的 Guid。

此外**PCPIN\_描述符**包括一个 GUID，可用于标识 pin 由唯一的名称。  GUID 存储在此 pin 名称**KsPinDescriptor.Name** PCPIN 成员\_描述符结构。 此名称使用 GUID ([**KSPROPERTY\_PIN\_名称**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)) 使用的 pin 在注册表中找到的属性可关联一个友好名称。 

调用音频子系统**KSPROPERTY\_PIN\_名称**属性将与音频终结点关联的友好名称。 KS 处理此请求通过注册表描述的 unicode 字符串的第一个搜索**KsPinDescriptor.Name** GUID。  如果 KS 不到的项，它将搜索 unicode 字符串描述的注册表**KsPinDescriptor.Category** GUID。  

从开始**Windows 10 REDSTONE 5**时搜索注册表，KS 首先查找中设备的软件密钥的条目。  创建方法是： 通过引用 [模型] 部分中的设备驱动程序的 INF AddReg 部分 INF。  AddReg 部分构造使用 HKR 这些条目\\MediaCategories 密钥。 GUID 是唯一的设备，还是不，这允许驱动程序开发人员创建名称和类别 Guid，特定于设备的友好名称。

如果未在设备的软件密钥中安装一个条目或驱动程序运行之前的操作系统上**Windows 10 REDSTONE 5**，在 HKLM 下看起来 KS\\系统\\CurrentControlSet\\控制\\MediaCategories 注册表项。 此第二个密钥将被视为全局命名空间。  从开始**Windows 10 REDSTONE 5**此空间将保留用于全局定义，不应修改的新驱动程序。  修改此项下的项将不支持在将来的操作系统版本。

公开与标准类别 Guid 的 pin 的音频设备应包含/需要收件箱 KS。INF 或 KSCAPTUR。设备 INF 中 INF 名称注册。  这些收件箱 Inf 包含默认的友好名称定义为您的驱动程序可能想要填充的预定义的类别 Guid。 这些是相同的 Guid 中找到**KsPinDescriptor.Category** PCPIN 成员\_描述符结构。 例如，类别 GUID KSNODETYPE\_麦克风项都有关联的友好名称"麦克风"和类别 GUID KSNODETYPE\_演讲者条目都具有关联的友好名称"发言人，"依次类推。

Guid 和友好名称的同时类别和名称 Guid 存储在 HKR\\MediaCategories 时全局定义 HKLM\\系统\\CurrentControlSet\\控制\\MediaCategories 路径。 在注册表中每个 GUID 名称对，为 GUID 字符串用作 MediaCategories 项下的子键。  在 GUID 项 Unicode 的友好名称下的字符串"Name"变量下的值。 

如果没有友好名称和 pin 类别定义的音频子系统充分描述你的设备，可以定义自己的 pin 类别和名称 Guid 以及你 INF 中与其关联的友好名称。 若要确保你的 pin 类别的 GUID 是唯一的使用 Uuidgen.exe 之类的实用工具生成的 GUID。 接下来，修改安装你音频适配器写入到注册表路径 HKR pin 类别 GUID 和友好名称的 INF 文件\\MediaCategories。 下面的代码示例显示了将两个 pin 类别 Guid 和其关联的友好名称添加到注册表的 INF 文件的片段：

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

这两个 GUID 字符串生成的 Uuidgen.exe。

应用程序可以通过使用设备的访问音频端点设备的属性**IPropertyStore**接口。 该界面使用 Functiondiscoverykeys 中定义的属性键\_devpkey.h 和 Mmdeviceapi.h 标头文件来标识属性。 应用程序可以使用**主键\_设备\_FriendlyName**属性键以检索终结点设备的友好名称。 为空间限制的用户界面的友好名称的较短版本可以检索通过使用**主键\_设备\_DeviceDesc**属性键。 有关这些属性密钥的详细信息，请参阅[IMMDevice::OpenPropertyStore](https://go.microsoft.com/fwlink/p/?linkid=155067)。

**IPropertyStore**接口的实例将保留的音频端点设备的持久属性存储区。 属性存储复制为其初始值**主键\_设备\_DeviceDesc**从与注册表路径 HKLMKSpin类别GUID关联的友好名称字符串的属性键\\系统\\CurrentControlSet\\控制\\MediaCategories。 应用程序可以读取**主键\_设备\_DeviceDesc**属性值 （名称字符串） 从属性存储，但它们不能更改此值。 但是，用户可以通过使用 Windows 多媒体控件面板 Mmsys.cpl 修改名称。 例如，在 Windows Vista 中，可以使用以下步骤来修改呈现终结点设备的名称：

1.  若要运行 Mmsys.cpl，打开命令提示符窗口并输入以下命令：

    ```console
    mmsys.cpl
    ```

    (或者，可以通过右键单击位于任务栏右侧，在通知区域中的扬声器图标，单击运行 Mmsys.cpl**播放设备**。)

2.  单击呈现设备的名称，然后单击**属性**。

3.  在属性窗口中，单击**常规**选项卡。在属性表顶部的文本框中应显示的友好名称。 可以编辑的友好名称，并单击，然后保存所做的更改**确定**。

在前面的步骤更改音频端点设备的属性存储中存储的友好名称。 这些步骤将不会影响与属于同一 KS pin 类别其他音频终结点设备相关联的友好名称。 它们还具有对任何组件，可以直接输入名称查询 KS 没有影响。
