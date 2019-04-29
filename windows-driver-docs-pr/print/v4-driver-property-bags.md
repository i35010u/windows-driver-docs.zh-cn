---
title: V4 打印机驱动程序属性包
description: V4 打印驱动程序模型提供了大量简化从自定义 UI 应用程序到呈现过程的数据流的属性包。
ms.assetid: 4E20303A-BEB3-4928-BA5A-356D978FA2BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6c12ec567d99dc8d96b1fc2dbae21352e0f41d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358566"
---
# <a name="v4-printer-driver-property-bags"></a>V4 打印机驱动程序属性包


V4 打印驱动程序模型提供了大量简化从自定义 UI 应用程序到呈现过程的数据流的属性包。

这些属性包允许自定义属性和功能定义要在自定义 UI 中创建，然后使用由呈现进程。 所有属性包通过使用都公开[ **IPrinterScriptablePropertyBag** ](https://msdn.microsoft.com/library/windows/hardware/hh973217)界面在 JavaScript 中或通过使用[ **IPrinterPropertyBag** ](https://msdn.microsoft.com/library/windows/hardware/hh439547)在其他环境中的接口。

下表概述了如何使用不同的组件来获取属性包对象从 v4 打印驱动程序的不同部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>JavaScript 约束脚本</td>
<td>驱动程序和队列属性包传递给 JavaScript 约束脚本使用 scriptContext 参数。 此参数的类型是<a href="https://msdn.microsoft.com/library/windows/hardware/hh768279" data-raw-source="[&lt;strong&gt;IPrinterScriptContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh768279)"> <strong>IPrinterScriptContext</strong> </a>和包含子项：驱动程序属性 – 表示驱动程序属性包。
QueueProperties – 表示队列属性包。
UserProperties – 用户属性包。
DEVMODE 属性包传递到 DEVMODE &lt; - &gt; PrintTicket 转换方法，例如<em>devModeProperties</em>参数 (它属于类型<strong>IPrinterScriptablePropertyBag</strong>)。 它将对其他方法不可用。</td>
</tr>
<tr class="even">
<td>USB Bidi JavaScript</td>
<td>驱动程序和队列属性包传递到 USB Bidi JavaScript 脚本使用 scriptContext 参数。 此参数的类型是<strong>IPrinterScriptContext</strong>和包含子项：驱动程序属性 – 表示驱动程序属性包。
QueueProperties – 表示队列属性包。</td>
</tr>
<tr class="odd">
<td>打印机扩展应用程序</td>
<td>所有属性包的一部分都传入<a href="https://msdn.microsoft.com/library/windows/hardware/hh973207" data-raw-source="[&lt;strong&gt;IPrinterExtensionEventArgs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh973207)"> <strong>IPrinterExtensionEventArgs</strong> </a> OnDriverEvent 处理程序的参数。 它们是类型的所有<strong>IPrinterPropertyBag</strong>。 被指定为以下：驱动程序属性 – 表示驱动程序属性包。
UserProperties – 用户属性包。
PrinterQueue.GetProperties() – 指队列属性包</td>
</tr>
<tr class="even">
<td>UWP 的设备应用程序</td>
<td>使用激活过程中的所有属性包都传递<a href="https://msdn.microsoft.com/library/windows/hardware/hh406649" data-raw-source="[&lt;strong&gt;IPrinterExtensionContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406649)"> <strong>IPrinterExtensionContext</strong> </a>对象。 被指定为：驱动程序属性 – 表示驱动程序属性包。
UserProperties – 用户属性包。
PrinterQueue.GetProperties() – 指队列属性包</td>
</tr>
<tr class="odd">
<td>XPS 呈现筛选器</td>
<td><p>XPS 筛选器可以从内部访问驱动程序属性包<a href="https://msdn.microsoft.com/library/windows/hardware/ff561066" data-raw-source="[&lt;strong&gt;Print Filter Pipeline Property Bag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561066)"><strong>打印筛选器管道属性包</strong></a>使用属性命名为"DriverPropertyBag"或从定义的值XPS_FP_PROPERTY_BAG<em>filterpipeline.h</em>。 下面是有关 DriverPropertyBag 信息：</p>
<strong>属性类型：</strong>VT_UNKNOWN<strong>说明：</strong>指向 IUnknown 接口的指针。 调用 QueryInterface 来获取驱动程序属性包的 IPrinterPropertyBag 接口的指针。
<p>XPS 筛选器可以访问队列属性包中使用属性名称"QueuePropertyBag"，或定义打印筛选器管道属性包和值从 XPS_FP_QUEUE_PROPERTY_BAG <em>filterpipeline.h</em>。 下面是有关 QueuePropertyBag 信息：</p>
<strong>属性类型：</strong>VT_UNKNOWN<strong>说明：</strong>指向 IUnknown 接口的指针。 调用 QueryInterface 来获取对队列的属性包的 IPrinterPropertyBag 接口的指针。</td>
</tr>
</tbody>
</table>



在 JavaScript 实现中，在作为参数传递属性包。 打印机扩展应用程序，在属性包传递中作为用于启动应用程序事件自变量的成员。

提供的 COM IPrinterQueue、 IPrinterExtensionContext 和 IPrinterExtensionEventArgs 接口的属性包访问器，以及在 Javascript 实现的属性包访问器将引发异常，如果未指定的属性包或找不到。 此外，查询 IPrinterPropertyBag 接口上的单个属性将引发异常，如果找不到该属性。 应使用 try catch 语句来避免崩溃如果属性不可用。

## <a name="driver-property-bag"></a>驱动程序属性包


驱动程序属性包是预定义属性或数据 blob 的只读、 只使用了由驱动程序的驱动程序的数据存储。 它可以通过在 v4 清单文件中使用"PropertyBag"指令指定并不能修改在运行时。

Windows 驱动程序工具包包括驱动程序属性包的模板项目。 驱动程序属性包是一个编译的二进制 blob。 Visual Studio 包含用于生成已编译的驱动程序属性包的模板。 为此模板生成的 XML 文件不是属性包，而是此模板的已编译的输出是应在 v4 清单文件中指定的属性包文件。

## <a name="user-property-bag"></a>用户属性包


用户属性包让合作伙伴可以将设置存储在每个用户、 计算机本地上下文。 此属性包非常适合用作用户首选项，如"不再显示此信息"的存储机制。 此属性包不是可由管理员管理和打印机共享期间客户端和服务器之间不同步。 用户属性包只能在运行时设置，并且仅可供打印机扩展、 UWP 设备应用和 JavaScript 约束。

**请注意**因为 JavaScript 约束也可能称为外部用户上下文中，在 despooling、 用户属性包这一次是不可用，Windows 将返回 HRESULT\_FROM\_WIN32 (错误\_不\_找到)。



## <a name="devmode-property-bag"></a>DEVMODE 属性包


DEVMODE 属性包用来组织 DEVMODE 结构的专用部分中的内容。 在 ConvertPrintTicketToDevMode 调用期间调用 JavaScript，以填充 DEVMODE 属性包的内容。 ConvertDevModeToPrintTicket 在调用期间，会调用 JavaScript 来从 DEVMODE 属性包读取持久化的设置，然后将其存储在 PrintTicket 返回。

此属性包的大小小于 60 KB （恰到好处的差异取决于已分配的 DEVMODE 节的大小），大小限制，因为它必须序列化为 DEVMODE 结构以避免数据丢失，在某些情况下。 因为由 DEVMODE 的公共部分加上配置模块管理的专用部分大小提供的确切大小将因驱动程序。

DEVMODE 属性包使用的 XML 文件指定的属性包的成员，并使用 convertPrintTicketToDevMode 和 convertDevModeToPrintTicket Api 来处理转换。 必须使用 DevModeMap 指令，v4 清单中指定 XML DEVMODE 映射文件。

下面的代码段显示了一个 DEVMODE 属性包映射 XML 示例。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns="http://schemas.microsoft.com/windows/2011/08/printing/devmodemap">
  <Property Name="FabrikamAccountCode">
    <String Length="32"></String>
  </Property>  
</Properties>
```

下面的屏幕截图显示了 DEVMODE 属性包映射 XML 架构，以及它在 WDK 安装文件夹中可从以下路径：\\Include\\um\\printerdriverdevmodemap.xsd.pr

![devmode 属性包映射 xml 架构](images/propbagmapschema.png)

DEVMODE 属性包映射的 XML 文件进行验证由 INFGate 工具。

## <a name="queue-property-bag"></a>队列属性包


队列属性包将存储每个队列配置设置，包括窗体送纸器映射和打印机属性，如可安装选项的配置。 驱动程序定义的属性和打印机属性是在 PowerShell 中，可配置，而是在 UI 中的打印机属性可配置的送纸器映射到窗体。 打印机扩展不能编辑的任何属性值。

队列属性包会自动创建有关许多 v4 打印驱动程序，但驱动程序还可能会提供其他属性使用的 XML 文件进行配置。 不应使用该驱动程序属性包工具编译此 XML 文件。 队列属性包是可用于执行以下任一操作的 v4 打印驱动程序支持的打印机：

1. 指定多个送纸器，或

2. 在 GPD 或 PPD 文件中，指定可安装选项或

3. 使用 QueueProperties 指令在驱动程序清单中指定的队列属性包。

管理员配置队列属性包使用 PowerShell。 以下命令-允许 (cmdlet) 是一个打印机对象，可以使用 Get 打印机 cmdlet 获取对象的子级。

| Cmdlet 名称                                                                                                  | 描述                                                             |
|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Get-PrinterProperty -printerName &lt;printerName&gt; -name &lt;propertyName\*&gt;                            | 检索一个或多个属性 (-名称支持通配)              |
| Set-PrinterProperty -inputObject &lt;printerPropertyObject&gt;                                               | 更改使用持久化的 printerPropertyObject 的打印队列属性。 |
| set-PrinterProperty -printerName &lt;printerName&gt; -PropertyName &lt;propertyName&gt; -Value &lt;value&gt; | 更改为指定的值指定的属性。                  |



**可安装选项**。 这些选项，例如，双面打印器，状态将作为单独的属性公开到队列的属性包。 如下所示，该功能名称基于从驱动程序的 GPD 或 PPD 文件功能的名称，将名为每个属性：

- Config:&lt;功能名称&gt;

例如，Config:DuplexUnit

属性的值是已由管理员选择的选项的关键字名称。 例如，安装。 可安装选项是编辑使用同一组 PrinterProperty cmdlet 用于队列属性。

**请注意**从 Windows 8.1 开始，具有管理员权限的用户或创建打印队列的用户可以更改可安装选项和队列属性包的每个队列配置设置从 UWP 设备应用。



**送纸器映射到窗体**。 使用 v4 打印机的打印驱动程序，并使用多个送纸器，可以通过名为"FormTrayTable"属性中的队列属性包中公开"窗体到任务栏"映射。

此属性的格式设置为以 null 结尾的字符串包含格式对"&lt;纸盒名&gt;，&lt;窗体名称&gt;，"窗体名称其中是以下值之一：

1. 如果纸张大小映射到 GPD 或 PPD 文件中的打印架构 (通过使用标准\*PaperSize /\*PageSize 关键字或\*（毫秒） PrintSchemaKeywordMap)，则窗体名称将遵循以下格式：

PrintSchema:&lt;纸张大小名称&gt;

例如，PrintSchema:NorthAmericaLetter

2. 如果窗体是用户定义的形式，由窗体\_用户标志，则窗体名称将是按如下所示。 窗体索引是在后台处理程序的窗体数据库中使用的相同值。 这是与索引的纸张大小指定为用户窗体 PrintTicket 中时使用一致&lt;窗体索引&gt;。

用户窗体&lt;窗体索引&gt;

例如，UserForm123

3. 否则，窗体名称将遵循以下格式，其中的窗体名称是 GPD 中指定的名称\*PaperSize 或 PPD \*PageSize。

Config:&lt;名称&gt;

例如，配置：\_8\_5 x 16

完整示例字符串将如下所示："Config:Tray1、 PrintSchema:NorthAmericaLetter、 Config:Tray2、 配置：\_8\_5 X 16，Config:Manual、 UserForm123，\\0"。

呈现的筛选器应读取传入 PrintTicket PageMediaSize 设置，并搜索 FormTrayTable 中的窗体名称值中的值。

**队列属性包的 XML 示例**。 下面的代码段显示了可用于以下三个属性、 Name1、 Name2，Name3 和它们的子元素的 XML 语法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns= "http://schemas.microsoft.com/windows/2011/08/printing/queueproperties">
  <Property Name="Name1">
    <String>String1</String>
  </Property>
  <Property Name="Name2">
    <Int32>3244</Int32>
  </Property>
  <Property Name="Name3">
    <Bool>true</Bool>
  </Property>
</Properties>
```

**队列属性包 XML 架构**。 下面的屏幕截图显示了队列属性包 XML 架构，以及它在 WDK 安装文件夹中可从以下路径：\\包括\\um\\printqueueproperties.xsd。

![队列属性包 xml 架构](images/queuepropbagschem.png)

## <a name="related-topics"></a>相关主题
[**IPrinterExtensionContext**](https://msdn.microsoft.com/library/windows/hardware/hh406649)  
[**IPrinterExtensionEventArgs**](https://msdn.microsoft.com/library/windows/hardware/hh973207)  
[**IPrinterPropertyBag**](https://msdn.microsoft.com/library/windows/hardware/hh439547)  
[**IPrinterScriptablePropertyBag**](https://msdn.microsoft.com/library/windows/hardware/hh973217)  
[**IPrinterScriptContext**](https://msdn.microsoft.com/library/windows/hardware/hh768279)  
[**打印筛选器管道属性包**](https://msdn.microsoft.com/library/windows/hardware/ff561066)  



