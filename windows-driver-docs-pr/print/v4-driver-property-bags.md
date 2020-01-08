---
title: V4 打印机驱动程序属性包
description: V4 打印驱动程序模型提供了许多属性包，便于从自定义 UI 应用程序到呈现过程的数据流。
ms.assetid: 4E20303A-BEB3-4928-BA5A-356D978FA2BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51919d93e288268d3456903eaac287b4ffeeb4a9
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653001"
---
# <a name="v4-printer-driver-property-bags"></a>V4 打印机驱动程序属性包


V4 打印驱动程序模型提供了许多属性包，便于从自定义 UI 应用程序到呈现过程的数据流。

这些属性包允许在自定义 UI 中创建自定义属性和功能定义，并由呈现进程使用。 所有属性包都通过使用 JavaScript 中的[**IPrinterScriptablePropertyBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)接口或在其他环境中使用[**IPrinterPropertyBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterpropertybag)接口公开。

下表概述了如何使用不同的组件从 v4 打印驱动程序的不同部分获取属性包对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>JavaScript 约束脚本</td>
<td>使用 scriptContext 参数将驱动程序和队列属性包传递到 JavaScript 约束脚本。 此参数的类型为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext" data-raw-source="[&lt;strong&gt;IPrinterScriptContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)"><strong>IPrinterScriptContext</strong></a> ，包含子级： DriverProperties –指驱动程序属性包。
QueueProperties –表示 queue 属性包。
UserProperties-用户属性包。
DEVMODE 属性包作为<em>devModeProperties</em>参数（其类型为<strong>IPrinterScriptablePropertyBag</strong>）传递到 Devmode &lt;-&gt; PrintTicket 转换方法。 其他方法不可用。</td>
</tr>
<tr class="even">
<td>USB 双向 JavaScript</td>
<td>使用 scriptContext 参数将驱动程序和队列属性包传递到 USB 双向 JavaScript 脚本。 此参数的类型为<strong>IPrinterScriptContext</strong> ，包含子级： DriverProperties –指驱动程序属性包。
QueueProperties –表示 queue 属性包。</td>
</tr>
<tr class="odd">
<td>打印机扩展应用程序</td>
<td>所有属性包都作为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs" data-raw-source="[&lt;strong&gt;IPrinterExtensionEventArgs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)"><strong>IPrinterExtensionEventArgs</strong></a>参数的一部分传递给 OnDriverEvent 处理程序。 它们都是<strong>IPrinterPropertyBag</strong>类型。 它们被指定为以下形式： DriverProperties –指驱动程序属性包。
UserProperties-用户属性包。
PrinterQueue. GetProperties （）–引用 queue 属性包</td>
</tr>
<tr class="even">
<td>UWP 设备应用</td>
<td>在激活过程中，将使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext" data-raw-source="[&lt;strong&gt;IPrinterExtensionContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext)"><strong>IPrinterExtensionContext</strong></a>对象传入所有属性包。 它们被指定为： DriverProperties –是指驱动程序属性包。
UserProperties-用户属性包。
PrinterQueue. GetProperties （）–引用 queue 属性包</td>
</tr>
<tr class="odd">
<td>XPS 呈现筛选器</td>
<td><p>XPS 筛选器可以使用属性名称 "DriverPropertyBag" 从 "<a href="https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag" data-raw-source="[&lt;strong&gt;Print Filter Pipeline Property Bag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)"><strong>打印筛选器管道" 属性包</strong></a>内访问驱动程序属性包，也可以从<em>filterpipeline</em>中 XPS_FP_PROPERTY_BAG 定义的值。 下面是有关 DriverPropertyBag 的信息：</p>
<strong>属性类型：</strong>VT_UNKNOWN<strong>说明：</strong>指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向驱动程序属性包的 IPrinterPropertyBag 接口的指针。
<p>和 XPS 筛选器可以使用属性名称 "QueuePropertyBag" 从 "打印筛选器管道" 属性包中访问队列属性包，或者从<em>filterpipeline</em>中 XPS_FP_QUEUE_PROPERTY_BAG 定义的值。 下面是有关 QueuePropertyBag 的信息：</p>
<strong>属性类型：</strong>VT_UNKNOWN<strong>说明：</strong>指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 queue 属性包的 IPrinterPropertyBag 接口的指针。</td>
</tr>
</tbody>
</table>



在 JavaScript 实现中，属性包作为参数传入。 在打印机扩展应用程序中，属性包作为事件参数的成员传入，用于启动应用程序。

如果未指定属性包，COM IPrinterQueue、IPrinterExtensionContext 和 IPrinterExtensionEventArgs 接口以及 Javascript 实现中的属性包访问器提供的属性包访问器将引发异常。或找不到。 此外，如果找不到该属性，则在 IPrinterPropertyBag 接口上查询各个属性将引发异常。 如果属性不可用，则应使用 try catch 语句来避免发生崩溃。

## <a name="driver-property-bag"></a>驱动程序属性包


驱动程序属性包是用于预定义属性的驱动程序的数据存储，也可以是用于由驱动程序以只读方式使用的数据 blob。 可以通过在 v4 清单文件中使用 "PropertyBag" 指令来指定它，并且在运行时可能不会修改它。

Windows 驱动程序工具包包含驱动程序属性包的模板项目。 驱动程序属性包是已编译的二进制 blob。 Visual Studio 包含一个用于生成编译的驱动程序属性包的模板。 为此模板生成的 XML 文件不是属性包，而是此模板的编译输出是应在 v4 清单文件中指定的属性包文件。

## <a name="user-property-bag"></a>用户属性包


用户属性包允许合作伙伴将设置存储在每个用户的本地上下文中。 此属性包非常适合用作用户首选项（如 "不再显示此类"）的存储机制。 此属性包不能由管理员管理，并且在打印机共享期间不会在客户端和服务器之间进行同步。 用户属性包仅在运行时设置，并且仅适用于打印机扩展、UWP 设备应用和 JavaScript 约束。

**注意** 由于 JavaScript 约束也可能在用户上下文之外调用，因此在 despooling 期间，用户属性包此时不可用，Windows 将从\_WIN32 返回 HRESULT\_（错误\_未\_找到）。



## <a name="devmode-property-bag"></a>DEVMODE 属性包


DEVMODE 属性包用于在 DEVMODE 结构的 private 节中组织内容。 在 ConvertPrintTicketToDevMode 调用过程中，将调用 JavaScript 来填充 DEVMODE 属性包的内容。 在 ConvertDevModeToPrintTicket 调用过程中，将调用 JavaScript 以从 DEVMODE 属性包读取持久设置并将其存储在 PrintTicket 中。

此属性包的大小限制为小于 60 KB （确切的数量因 DEVMODE 分配部分的大小而异），因为它必须序列化为 DEVMODE 结构，以避免在某些情况下丢失数据。 每个驱动程序的可用确切大小会有所不同，因为它是由 DEVMODE 的 public 部分的大小和配置模块管理的私有部分确定的。

DEVMODE 属性包使用 XML 文件来指定属性包的成员，并使用 convertPrintTicketToDevMode 和 convertDevModeToPrintTicket Api 来处理转换。 必须使用 DevModeMap 指令在 v4 清单中指定 XML DEVMODE 映射文件。

下面的代码段演示了 DEVMODE 属性包映射 XML 示例。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns="https://schemas.microsoft.com/windows/2011/08/printing/devmodemap">
  <Property Name="FabrikamAccountCode">
    <String Length="32"></String>
  </Property>  
</Properties>
```

以下屏幕截图显示了 DEVMODE 属性包映射 XML 架构，并可在 WDK 安装文件夹中找到以下路径： \\包括\\um\\printerdriverdevmodemap.xsd.pr

![devmode 属性包映射 xml 架构](images/propbagmapschema.png)

DEVMODE 属性包映射的 XML 文件由 INFGate 工具验证。

## <a name="queue-property-bag"></a>队列属性包


队列属性包存储每个队列的配置设置，包括窗体到托盘映射和打印机属性（如可安装选项）的配置。 驱动程序定义的属性和打印机属性在 PowerShell 中是可配置的，而窗体到托盘的映射可以在打印机属性 UI 中进行配置。 打印机扩展无法编辑任何属性值。

队列属性包是为多个 v4 打印驱动程序自动创建的，但驱动程序还可以提供其他属性以使用 XML 文件进行配置。 不应使用驱动程序属性包工具编译此 XML 文件。 队列属性包可用于 v4 打印驱动程序支持的打印机，这些驱动程序执行以下任一操作：

1. 指定多个纸盒，或

2. 指定 GPD 或 PPD 文件中的可安装选项，或

3. 使用 QueueProperties 指令在驱动程序清单中指定队列属性包。

管理员使用 PowerShell 配置 queue 属性包。 以下命令-允许（cmdlet）是打印机对象的子项，可以使用 "打印机" cmdlet 获取该对象。

| Cmdlet 名称                                                                                                  | 描述                                                             |
|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| PrinterProperty-printerName &lt;printerName&gt;-name &lt;propertyName\*&gt;                            | 检索一个或多个属性（-name 支持通配）              |
| PrinterProperty-inputObject &lt;printerPropertyObject&gt;                                               | 使用持久化 printerPropertyObject 更改打印队列属性。 |
| PrinterProperty-printerName &lt;printerName&gt;-PropertyName &lt;属性名称&gt;-值 &lt;值&gt; | 将指定的属性更改为指定的值。                  |



可**安装选项**。 例如，双面打印器的状态将作为单个属性公开给队列属性包。 每个属性的名称如下所示，其中的功能名称基于驱动程序的 GPD 或 PPD 文件中的功能名称：

- Config：&lt;功能名称&gt;

例如，Config： DuplexUnit

属性的值是管理员已选择的选项的关键字名称。 例如，已安装。 可使用用于队列属性的 PrinterProperty cmdlet 编辑可安装选项。

**注意** 从 Windows 8.1 开始，拥有管理员权限的用户或创建打印队列的用户可以更改 UWP 设备应用中队列属性包的可安装选项和每队列配置设置。



**窗体到托盘映射**。 对于带有 v4 打印驱动程序的打印机和多个送纸器，可以通过名为 "FormTrayTable" 的属性中的队列属性包公开 "窗体到托盘" 映射。

此属性的格式为以 null 结尾的字符串，该字符串包含格式为 "&lt;托盘名称&gt;，&lt;窗体名称&gt;"，其中窗体名称是以下内容之一：

1. 如果纸张大小在 GPD 或 PPD 文件中映射到打印架构（通过使用标准 \*PaperSize/\*PageSize 关键字或 \*（MS） PrintSchemaKeywordMap），则窗体名称将遵循以下格式：

PrintSchema：&lt;纸张大小名称&gt;

例如，PrintSchema： NorthAmericaLetter

2. 如果窗体是用户定义的窗体（由窗体\_用户标志确定），则窗体名称将如下所示。 窗体索引与后台处理程序的窗体数据库中使用的值相同。 这与在 PrintTicket 中以用户窗体&lt;窗体索引&gt;在 PrintTicket 中指定纸张大小时使用的索引一致。

窗体&lt;窗体索引&gt;

例如，UserForm123

3. 否则，窗体名称将遵循以下格式，其中 form name 为 GPD 的 \*PaperSize 或 PPD 的 \*PageSize 中指定的名称。

Config：&lt;名称&gt;

例如，Config：\_8\_5x16

下面是一个完整的示例字符串，如下所示： "Config： Tray1，PrintSchema： NorthAmericaLetter，Config： Tray2，Config：\_8\_5X16，Config： Manual，UserForm123，\\0"。

呈现筛选器应读取传入的 PrintTicket 的 PageMediaSize 设置，并在 FormTrayTable 的名称值中搜索该值。

**队列属性包 XML 示例**。 以下代码段显示了可用于三个属性、Name1、Name2、Name3 及其子元素的 XML 语法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns= "https://schemas.microsoft.com/windows/2011/08/printing/queueproperties">
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

**队列属性包 XML 架构**。 以下屏幕截图显示队列属性包 XML 架构，并可在 WDK 安装文件夹中找到以下路径： \\包括\\um\\printqueueproperties。

![队列属性包 xml 架构](images/queuepropbagschem.png)

## <a name="related-topics"></a>相关主题
[**IPrinterExtensionContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext)  
[**IPrinterExtensionEventArgs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)  
[**IPrinterPropertyBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterpropertybag)  
[**IPrinterScriptablePropertyBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)  
[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  
[**打印筛选器管道属性包**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)  



