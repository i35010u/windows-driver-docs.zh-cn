---
title: V4 驱动程序清单
description: V4 打印驱动程序清单包含特定于打印机的安装程序指令和使用 INF 文件结合使用。
ms.assetid: 187A10B7-2AAC-46D9-998C-C8724D8E3862
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78dce61c66569d7c25282704c4cf3323506007df
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161538"
---
# <a name="v4-driver-manifest"></a>V4 驱动程序清单


V4 打印驱动程序清单是包含所有特定于打印机的安装程序指令的文本文件。 V4 打印驱动程序清单是结合使用 v4 打印驱动程序 INF 文件后，作为集的一部分为特定于打印机的 v4 打印驱动程序。

在清单中的指令划分为部分：

-   [DriverConfig Section](#driverconfig-section)
-   [BidiFiles 部分](#bidifiles-section)
-   [DriverRender 部分](#driverrender-section)
-   [存部分](#filesave-section)
-   [PrinterExtensions 部分](#printerextensions-section)
-   [相关主题](#related-topics)

## <a name="driverconfig-section"></a>DriverConfig 部分


下表显示了 DriverConfig 节中使用的指令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令</th>
<th>限制</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>RequiredFiles</strong></p>
<p>包括 ntprint.inf 或 ntprint4.inf 中的文件。</p>
<p>Windows 10 中的下，RequiredFiles 指令将支持以下值：</p>
<p>PWGRRenderFilter.dll:将 Microsoft PWG 光栅呈现筛选器添加到驱动程序的依赖文件列表。</p>
<p>PWG 光栅呈现筛选器呈现筛选器要求驱动程序配置为使用 PrintDeviceCapabilities 文件。</p></td>
<td><p>此列表中，应省略 Unidrv.dll、 pscript5.dll 和 mxdwdrv.dll。 它们将被自动解决。</p></td>
<td><p>示例：</p>
<p>下，RequiredFiles =</p>
<p>UNIRES.DLL,STDNAMES.GPD,</p>
<p>V3HOSTINGFILTER.DLL</p></td>
</tr>
<tr class="even">
<td><p><strong>RequiredClass</strong></p>
<p>导致此驱动程序，包括从已定义的类驱动程序使用的设备和其 GUID 的驱动程序/友好名称作为键的所有文件。 这是用于将 printclass 驱动程序链接到模型特定驱动程序的机制。</p></td>
<td><p>RequiredClass 指令不能使用由类驱动程序。 当使用 RequiredClass 时，应避免文件之间的打印机驱动程序和打印类驱动程序所链接的名称冲突。</p>
<p>尽管具有类似名称的文件不会相互覆盖，但它可能很难在疑难解答期间，若要区分类驱动程序包文件和 v4 打印机驱动程序中的文件。</p></td>
<td><p>例如：</p>
<p>RequiredClass =</p>
<p>"Fabrikam PCL5e Class Driver",{9343720D-B67E-4451-B93F-6F721C439771}</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverFile</strong></p>
<p>这将指向二进制的呈现。 Mxdwdrv 是默认值，但类驱动程序或者可能指定 unidrv.dll 或 pscript5.dll。 这是功能上等同于在同一指令中 v3 INF。</p></td>
<td><p>只能在类驱动程序设置。 有效选项为 unidrv.dll 或 pscript5.dll。 V4 打印驱动程序或者从继承 RequiredClass 或默认值为 mxdwdrv.dll</p></td>
<td><p>DriverFile=</p>
<p>unidrv.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFile</strong></p>
<p>这定义主 GPD 或 PPD 此驱动程序。 这是功能上等同于在同一指令中 v3 INF。</p>
<p>在 Windows 10 中，v4 打印驱动程序可以继续指定 GPD 或 PPD 数据文件，但是，它们还可以描述即 PrintDeviceCapabilities 格式数据文件。</p></td>
<td><p>必需。</p></td>
<td><p>示例：</p>
<p>DataFile=FAPDL.gpd</p>
<p>DataFile=FAPDL.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>DataFileType</strong></p>
<p>此外为数据文件，并且可能描述 PrintDeviceCapabilities 文件与 GPD 或基于 PPD 的数据文件也一起使用时，必须使用 DataFileType。</p></td>
<td><p>PrintDeviceCapabilities 文件所需。</p></td>
<td><p>例如：</p>
<p>DataFileType=</p>
<p>"application/vnd.ms-PrintDeviceCapabilities+xml"</p></td>
</tr>
<tr class="even">
<td><p><strong>标志</strong></p>
<p>这用于指定与该驱动程序相关联的附加的可选属性。</p>
<p></p>
NotShareable:此标志指定驱动程序不是可共享。 这是合适的虚拟驱动程序，如 Microsoft XPS Document Writer。
SoftResetOnJobCancellation:此标志指定设备需要 USB 软重置 (IOCTL_USBPRINT_SOFT_RESET) 上的打印作业取消。
ArchiveEnabled v4 驱动程序使用此标志请求作为后台打印文件存档优化 XPS。</td>
<td><p>无。</p></td>
<td><p>示例：</p>
<p>标志 =</p>
<p>NotShareable，</p>
<p>SoftResetOnJobCancellation</p>
<p>标志 =</p>
<p>ArchiveEnabled NotShareable</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrinterDriverID</strong></p>
<p>这是描述打印驱动程序的唯一 ID。 如果两个驱动程序指定相同 PrinterDriverID，它们必须兼容的共享和支持的相同打印机扩展。</p></td>
<td><p>必需。</p></td>
<td><p>PrinterDriverID=</p>
<p>{guid}</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyBag</strong></p>
<p>指定此驱动程序的驱动程序属性包。 这是由 DriverPropertyBagTool.exe 或 Visual Studio 生成的已编译的文件。</p></td>
<td><p>无。</p></td>
<td><p>PropertyBag =</p>
<p>FAProperty.dpb</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResourceFile</strong></p>
<p>定义驱动程序的字符串资源 DLL 的名称。</p>
<p>在 Windows 10 中，驱动程序可以指定使用.resx 格式 ResourceFile。</p></td>
<td><p>无。</p></td>
<td><p>示例：</p>
<p>ResourceFile=</p>
<p>FARC.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>ConstraintScript</strong></p>
<p>定义在驱动程序的 JavaScript 约束文件的名称。</p></td>
<td><p>无。</p></td>
<td><p>ConstraintScript=</p>
<p>FAConst.js</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverCategory</strong></p>
<p>定义多个选项之一在设备的类别。 有效选项如下所示：</p>
PrintFax.Fax PrintFax.Printer PrintFax.Printer.3D PrintFax.Printer.File PrintFax.Printer.Service PrintFax.Printer.Virtual</td>
<td><p>必需。</p></td>
<td><p>DriverCategory=</p>
<p>PrintFax.Printer</p>
<p>有关其他驱动程序类别的详细信息，请参阅<a href="printer-inf-file-entries.md" data-raw-source="[Printer INF File Entries](printer-inf-file-entries.md)">打印机 INF 文件条目</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>PrinterExtensionUrl</strong></p>
<p>指定用户要获得一份打印机扩展应用程序的 URL。 在打印机共享中使用。</p></td>
<td><p>无。</p></td>
<td><p>PrinterExtensionUrl=</p>
<p>"<a href="http://www.fabrikam.com/files/setup.exe&quot" data-raw-source="http://www.fabrikam.com/files/setup.exe&quot">http://www.fabrikam.com/files/setup.exe&quot</a>;</p></td>
</tr>
<tr class="odd">
<td><p><strong>DevModeMap</strong></p>
<p>指定 Devmode 映射文件。 这是用于 PrintTicket 到 DEVMODE 转换中的 JavaScript 代码的 XML 文件。</p></td>
<td><p>无。</p></td>
<td><p>DevModeMap=</p>
<p>fadmmap.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>EventFile</strong></p>
<p>指定驱动程序事件 XML 文件。</p></td>
<td><p>无。</p></td>
<td><p>EventFile=</p>
<p>faevents.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>QueueProperties</strong></p>
<p>指定队列属性包的格式。 这是一个 XML 文件并不编译。</p></td>
<td><p>无。</p></td>
<td><p>QueueProperties=</p>
<p>faQueueProps.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBStatusInterface</strong></p>
<p>指定硬件 Id 相匹配要用于对 USB Bidi 通信的一个或多个设备接口的列表。</p></td>
<td><p>无，但如果状态通过不是打印接口的 USB 接口执行此操作应仅支持。</p></td>
<td><p>BidiUSBStatusInterface=</p>
<p>”USB\vid_1234&pid_1234”,</p>
<p>”USB\vid_1234&pid_4567”</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserPropertyBagScope</strong></p>
<p>此指令作为队列或制造商指定的用户属性包的作用域。</p>
<p>如果省略此指令，则队列将是默认值。 此指令的有效选项如下所示：</p>
队列：这是默认配置中，并且它与 Windows 8 行为一致。
制造商：所有队列在 INF 中使用相同制造商字符串都使用相同的用户属性包。</td>
<td><p>无。</p></td>
<td><p>UserPropertyBagScope=</p>
<p>制造商</p></td>
</tr>
<tr class="even">
<td><p><strong>RetrievePrintDeviceCapabilitiesFromDevice</strong></p>
<p>v4 驱动程序可能会指定，它们必须从 WS 打印 v2.0 打印机中检索 PrintDeviceCapabilities 文件，只要他们将 PrintDeviceCapabilities 文件设置为驱动程序的数据文件和 DataFileType 还指示数据文件的 MIME 类型"应用程序/vnd.ms-PrintDeviceCapabilities + xml"。 有效选项：</p>
<p>有效选项：</p>
<p>True:允许驱动程序的本地数据文件使用来自设备的 PrintDeviceCapabilities 文件替换。</p>
<p>False:驱动程序的本地数据文件不会替换与 PrintDeviceCapabilities 文件从设备中。</p>
<p>如果未指定，此指令的默认值为 false。</p></td>
<td><p>无。</p></td>
<td><p>例如：</p>
<p>RetrievePrintDeviceCapabilitiesFromDevice=</p>
<p>true</p></td>
</tr>
</tbody>
</table>

 

## <a name="bidifiles-section"></a>BidiFiles 部分


BidiFiles 部分用于定义 Bidi 扩展名为的文件。 它等同于 TCP 和 WSD 的 Windows 7 格式。 USB 关键字是新功能。

下表显示了 BidiFiles 节中使用的指令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令</th>
<th>限制</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BidiSPMFile</strong></p>
<p>此项定义的基于 IP 的打印机的 Bidi 扩展文件。</p></td>
<td><p>无。</p></td>
<td><p>BidiSPMFile=FaBidiSPM.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiWSDFile</strong></p>
<p>这将定义基于 WSD 的打印机的 Bidi 扩展文件。</p></td>
<td><p>无。</p></td>
<td><p>BidiWSDFile=FABidiWSD.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>BidiUSBFile</strong></p>
<p>这将为 USB 定义 Bidi 扩展。</p></td>
<td><p>无。</p></td>
<td><p>BidiUSBFile=FABidiUSB.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBJSFile</strong></p>
<p>这将为 USB 定义 JavaScript 扩展。</p></td>
<td><p>无。</p></td>
<td><p>BidiUSBJSFile=FABidiUSBJS.js</p></td>
</tr>
</tbody>
</table>

 

## <a name="driverrender-section"></a>DriverRender 部分


下表显示了 DriverRender 节中使用的指令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令</th>
<th>限制</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PageOutputQuality.[OptionName]</strong></p>
<p>更改图像压缩基于 PageOutputQuality 作业 PrintTicket 中的值</p></td>
<td><p>选项名称必须是标准 PrintSchema 命名空间中指定的名称。</p></td>
<td><p>PageOutputQuality.Draft=</p>
<p>MxdcImageType.JPEGHigh</p>
<p>PageOutputQuality.Normal=</p>
<p>MxdcImageType.JPEGMedium</p>
<p>PageOutputQuality.High=</p>
<p>MxdcImageType.PNG</p></td>
</tr>
<tr class="even">
<td><p><strong>XpsFormat</strong></p>
<p>更改打印此驱动程序的系统生成的 XPS 格式。 可以指定多个值，顺序表示驱动程序的首选项。</p></td>
<td><p>在使用 Unidrv/PScript 呈现的类驱动程序中使用不可用。</p></td>
<td><p>XpsFormat=XPS</p>
<p>XpsFormat=OpenXPS</p>
<p>XPSFormat=OpenXPS,XPS</p>
<p>XPSFormat=XPS,OpenXPS</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputFormat</strong></p>
<p>OutputFormat 指令描述单个 PDL 生成此驱动程序使用 MIME 类型。</p>
<p>将 WSD 打印机的 CreateJob 或 CreateJob2 操作期间使用此信息。</p></td>
<td><p>无。</p></td>
<td><p>有效的用法类型包括：</p>
<p>OutputFormat=</p>
<p>"应用程序/oxps"</p>
<p>OutputFormat=</p>
<p>"application/vnd.ms-xpsdocument"</p>
<p>OutputFormat=</p>
<p>"image/pwg-raster"</p>
<p>OutputFormat=</p>
<p>"application/vnd.ms-3mfdocument"</p>
<p>此外在此处指定任何其他有效定义的 MIME 类型。</p></td>
</tr>
</tbody>
</table>

 

PageOutputQuality 指令 MxdcImageType 关键字具有以下允许的值：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>MxdcImageType 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGHigh</strong></p>
<p>高压缩 JPEG （较小的文件）</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.JPEGMedium</strong></p>
<p>中的 JPEG 压缩</p></td>
</tr>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGLow</strong></p>
<p>低压缩 JPEG</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.PNG</strong></p>
<p>PNG 文件类型 （最大文件）</p></td>
</tr>
</tbody>
</table>

 

## <a name="filesave-section"></a>存部分


本部分中支持的文件保存方案。 本部分针对新 PORTPROMPT 端口类型安装 v4 打印驱动程序时，指定要在中显示的文件扩展名**常见文件**窗口中，同时指定了支持的可本地化资源字符串扩展和对话框本身。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令</th>
<th>限制</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>&lt;FileExtensionName&gt;</strong></p>
<p>此指令介绍使用 PORTPROMPT 端口此驱动程序中保存文件时要使用文件扩展名。 值是从驱动程序的 ResourceFile resourceID。 有关 XPS 和仅 OXPS，可以指定 0 的 resourceID 和打印后台处理程序将使用其内部资源，这些。</p></td>
<td><p>无。</p></td>
<td><p>&lt;FileExtensionName&gt;=</p>
<p>&lt;resourceID&gt;</p>
<p>Xps=1234</p></td>
</tr>
<tr class="even">
<td><p><strong>SaveAsTitle</strong></p>
<p>此指令介绍用于在保存文件对话框的标题。 值是从驱动程序的 ResourceFile resourceID。</p></td>
<td><p>无。</p></td>
<td><p>SaveAsTitle=</p>
<p>&lt;resourceID&gt;</p>
<p>SaveAsTitle=</p>
<p>4321</p></td>
</tr>
</tbody>
</table>

 

## <a name="printerextensions-section"></a>PrinterExtensions 部分


PrinterExtensions 部分指定打印机扩展和它支持的调用模式。 对于这两个条目，打印系统将自动注册该应用程序。 此外，应用程序将使用两个不同的参数，PrinterDriverID 和 ReasonID，按此顺序配置。 因此，每个条目必须使用不同的 PrinterExtensionID GUID。

下表显示了 PrinterExtensions 节中使用的指令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令</th>
<th>限制</th>
<th>用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DriverEvent</strong></p>
<p>维护 DriverEvent 模式的应用。</p></td>
<td><p>无。</p></td>
<td><p>DriverEvent=</p>
<p>app.exe,{extensionID GUID}</p></td>
</tr>
<tr class="even">
<td><p><strong>PrintPreferences</strong></p>
<p>维护 PrintPreferences 模式的应用。</p></td>
<td><p>无。</p></td>
<td><p>PrintPreferences=</p>
<p>app.exe，{extensionID GUID}</p></td>
</tr>
</tbody>
</table>

 

以下是一个示例的 v4 打印驱动程序清单。

```INF
[DriverConfig]
DataFile=FAPDL.xml
RequiredFiles=UNIRES.DLL,STDNAMES.GPD,STDDTYPE.GDL,STDSCHEM.GDL,STDSCHMX.GDL,XPSSVCS.DLL,MSXPSINC.GPD,PWGRRenderFilter.DLL
ResourceFile=FARC.dll
PropertyBag=FAProperty.dpb
PrinterDriverID={GUID}
DriverCategory=PrintFax.Printer
ConstraintScript=faconst.js
EventFile=faevents.xml
PrinterExtensionUrl="http://www.fabrikam.com/download.asp?uiapp=120"
UserPropertyBagScope=Manufacturer
DataFileType="application/vnd.ms-PrintDeviceCapabilities+xml"
RetrievePrintDeviceCapabilitiesFromDevice=true

[BidiFiles]
BidiSPMFile=FABidiSPM.xml
BidiWSDFile=FABidiWSD.xml
BidiUSBFile=FaBidiUSB.xml
BidiUSBJSFile=FABidiUSBJS.js

[DriverRender]
PageOutputQuality.Draft=MxdcImageType.JPEGHigh
PageOutputQuality.Normal=MxdcImageType.JPEGMedium
PageOutputQuality.High=MxdcImageType.PNG
OutputFormat="image/pwg-raster"

[PrinterExtensions]
DriverEvent=FAapp.exe,{GUID}
PrintPreferences=FAapp.exe,{GUID2}
```

## <a name="related-topics"></a>相关主题
[打印机 INF 文件条目](printer-inf-file-entries.md)  



