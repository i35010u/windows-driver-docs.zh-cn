---
title: V4 驱动程序清单
description: V4 打印驱动程序清单包含特定于打印机的安装指令，并与 INF 文件一起使用。
ms.assetid: 187A10B7-2AAC-46D9-998C-C8724D8E3862
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4545a2d88efdb04cff3c61eed755dfd12f2b578c
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662405"
---
# <a name="v4-driver-manifest"></a>V4 驱动程序清单


V4 打印驱动程序清单是一个文本文件，其中包含所有打印机特定的安装指令。 V4 打印驱动程序清单与 v4 打印驱动程序 INF 文件一起使用，这是为特定于打印机的 v4 打印驱动程序设置的一部分。

清单中的指令划分为多个部分：

-   [DriverConfig 部分](#driverconfig-section)
-   [BidiFiles 部分](#bidifiles-section)
-   [DriverRender 部分](#driverrender-section)
-   [FileSave 部分](#filesave-section)
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
<th>使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>RequiredFiles</strong></p>
<p>包括 ntprint.inf 或 ntprint4 中的文件。</p>
<p>RequiredFiles 指令将支持 Windows 10 中的以下值：</p>
<p>PWGRRenderFilter.dll：向驱动程序的依赖文件列表添加 Microsoft PWG 光栅呈现筛选器。</p>
<p>PWG 光栅呈现筛选器呈现筛选器需要驱动程序使用 PrintDeviceCapabilities 文件进行配置。</p></td>
<td><p>应从此列表中省略 Unidrv.dll、pscript5.dll 和 mxdwdrv.dll。 它们将自动得到解决。</p></td>
<td><p>示例：</p>
<p>RequiredFiles =</p>
<p>UNIRES.DLL STDNAMES。GPD,</p>
<p>V3HOSTINGFILTER.DLL</p></td>
</tr>
<tr class="even">
<td><p><strong>RequiredClass</strong></p>
<p>使此驱动程序包括定义的类驱动程序中的所有文件，并使用设备的驱动程序/友好名称及其 GUID 作为密钥。 这是将 printclass 驱动程序链接到模型特定驱动程序的机制。</p></td>
<td><p>类驱动程序无法使用 RequiredClass 指令。 当使用 RequiredClass 时，应避免在要链接到的打印机驱动程序和打印类驱动程序之间出现文件名冲突。</p>
<p>尽管具有相似名称的文件不会相互覆盖，但在故障排除过程中可能难以区分类驱动程序包文件和 v4 打印机驱动程序中的文件。</p></td>
<td><p>示例：</p>
<p>RequiredClass =</p>
<p>"Fabrikam PCL5e 类驱动程序"，{9343720D-B67E-4451-B93F-6F721C439771}</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverFile</strong></p>
<p>这将指向呈现二进制文件。 Mxdwdrv 是默认值，但类驱动程序可以另外指定 unidrv.dll 或 pscript5.dll。 此功能与 v3 INF 中的相同指令功能相同。</p></td>
<td><p>只能在类驱动程序中设置。 有效选项为 unidrv.dll 或 pscript5.dll。 V4 打印驱动程序继承自 RequiredClass 或 default 到 mxdwdrv.dll</p></td>
<td><p>DriverFile =</p>
<p>unidrv.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>数据</strong></p>
<p>这将为此驱动程序定义主 GPD 或 PPD。 此功能与 v3 INF 中的相同指令功能相同。</p>
<p>在 Windows 10 中，v4 打印驱动程序可能会继续指定 GPD 或 PPD 数据文件，但是，它们还可以描述采用 PrintDeviceCapabilities 格式的数据文件。</p></td>
<td><p>必需。</p></td>
<td><p>示例：</p>
<p>数据文件 = FAPDL. gpd</p>
<p>数据文件 =FAPDL.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>DataFileType</strong></p>
<p>将 PrintDeviceCapabilities 文件描述为数据文件时，必须使用 DataFileType，也可将其用于 GPD 或基于 PPD 的数据文件。</p></td>
<td><p>对于 PrintDeviceCapabilities 文件是必需的。</p></td>
<td><p>示例：</p>
<p>DataFileType =</p>
<p>"application/vnd.apple.mpegurl. ms-PrintDeviceCapabilities + xml"</p></td>
</tr>
<tr class="even">
<td><p><strong>标记</strong></p>
<p>这用于指定与驱动程序关联的其他可选属性。</p>
<p></p>
NotShareable：此标志指定该驱动程序不可共享。 这适用于虚拟驱动程序，如 Microsoft XPS 文档编写器。
SoftResetOnJobCancellation：此标志指定设备需要 USB 软重置 (IOCTL_USBPRINT_SOFT_RESET 打印作业取消) 。
ArchiveEnabled v4 驱动程序使用此标志将存档优化的 XPS 作为假脱机文件请求。</td>
<td><p>无。</p></td>
<td><p>示例：</p>
<p>Flags =</p>
<p>NotShareable,</p>
<p>SoftResetOnJobCancellation</p>
<p>Flags =</p>
<p>ArchiveEnabled,NotShareable</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrinterDriverID</strong></p>
<p>这是描述打印驱动程序的唯一 ID。 如果两个驱动程序指定了相同的 PrinterDriverID，则它们必须与共享兼容，并支持相同的打印机扩展。</p></td>
<td><p>必需。</p></td>
<td><p>PrinterDriverID =</p>
<p>guid.empty</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyBag</strong></p>
<p>指定此驱动程序的驱动程序属性包。 这是 DriverPropertyBagTool.exe 或 Visual Studio 生成的已编译文件。</p></td>
<td><p>无。</p></td>
<td><p>PropertyBag =</p>
<p>FAProperty.dpb</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResourceFile</strong></p>
<p>定义驱动程序的字符串资源 DLL 的名称。</p>
<p>在 Windows 10 中，驱动程序可以使用 .resx 格式指定 ResourceFile。</p></td>
<td><p>无。</p></td>
<td><p>示例：</p>
<p>ResourceFile =</p>
<p>FARC.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>ConstraintScript</strong></p>
<p>定义驱动程序的 JavaScript 约束文件的名称。</p></td>
<td><p>无。</p></td>
<td><p>ConstraintScript =</p>
<p>FAConst.js</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverCategory</strong></p>
<p>在多个选项中的一个选项之间定义设备的类别。 有效选项如下所示：</p>
PrintFax PrintFax PrintFax PrintFax. printer PrintFax.. e e. printer. printer。</td>
<td><p>必需。</p></td>
<td><p>DriverCategory =</p>
<p>PrintFax.Printer</p>
<p>有关其他驱动程序类别的详细信息，请参阅 <a href="printer-inf-file-entries.md" data-raw-source="[Printer INF File Entries](printer-inf-file-entries.md)">打印机 INF 文件条目</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>PrinterExtensionUrl</strong></p>
<p>指定一个 URL，用户可以使用该 URL 来获取打印机扩展应用程序的副本。 用于打印机共享。</p></td>
<td><p>无。</p></td>
<td><p>PrinterExtensionUrl =</p>
<p>"https://www.fabrikam.com/files/setup.exe";</p></td>
</tr>
<tr class="odd">
<td><p><strong>DevModeMap</strong></p>
<p>指定 Devmode 映射文件。 这是一个 XML 文件，与 PrintTicket 一起用于 JavaScript 代码中的 DEVMODE 转换。</p></td>
<td><p>无。</p></td>
<td><p>DevModeMap =</p>
<p>fadmmap.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>EventFile</strong></p>
<p>指定驱动程序事件 XML 文件。</p></td>
<td><p>无。</p></td>
<td><p>EventFile =</p>
<p>faevents.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>QueueProperties</strong></p>
<p>指定队列属性包的格式。 这是一个 XML 文件，不能进行编译。</p></td>
<td><p>无。</p></td>
<td><p>QueueProperties =</p>
<p>faQueueProps.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBStatusInterface</strong></p>
<p>指定与要用于 USB 双向通信的一个或多个设备接口匹配的硬件 Id 列表。</p></td>
<td><p>无，但仅当通过不是打印接口的 USB 接口完成状态时才支持。</p></td>
<td><p>BidiUSBStatusInterface =</p>
<p>"USB \ vid_1234&pid_1234"，</p>
<p>"USB \ vid_1234&pid_4567"</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserPropertyBagScope</strong></p>
<p>此指令将用户属性包的作用域指定为队列或制造商。</p>
<p>如果省略该指令，则 Queue 为默认值。 此指令的有效选项如下所示：</p>
Queue：这是默认配置，它与 Windows 8 行为匹配。
制造商：在 INF 中使用相同制造商字符串的所有队列均使用相同的用户属性包。</td>
<td><p>无。</p></td>
<td><p>UserPropertyBagScope =</p>
<p>制造商</p></td>
</tr>
<tr class="even">
<td><p><strong>RetrievePrintDeviceCapabilitiesFromDevice</strong></p>
<p>v4 驱动程序可以指定它们必须检索 WS 打印 v2.0 打印机中的 PrintDeviceCapabilities 文件，前提是它们将 PrintDeviceCapabilities 文件设置为驱动程序的数据文件，而 DataFileType 还表明数据文件属于 MIME 类型 "application/vnd.apple.mpegurl. ms-PrintDeviceCapabilities + xml"。 有效选项：</p>
<p>有效选项：</p>
<p>True：允许将驱动程序的本地数据文件替换为设备上的 PrintDeviceCapabilities 文件。</p>
<p>False：不会将驱动程序的本地数据文件替换为设备中的 PrintDeviceCapabilities 文件。</p>
<p>如果未指定，则此指令的默认值为 false。</p></td>
<td><p>无。</p></td>
<td><p>示例：</p>
<p>RetrievePrintDeviceCapabilitiesFromDevice =</p>
<p>是</p></td>
</tr>
</tbody>
</table>

 

## <a name="bidifiles-section"></a>BidiFiles 部分


BidiFiles 节用于定义双向扩展文件。 它与适用于 TCP 和 WSD 的 Windows 7 格式完全相同。 USB 关键字是新的。

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
<th>使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BidiSPMFile</strong></p>
<p>这将为基于 TCP/IP 的打印机定义双向扩展文件。</p></td>
<td><p>无。</p></td>
<td><p>BidiSPMFile =FaBidiSPM.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiWSDFile</strong></p>
<p>这将为基于 WSD 的打印机定义双向扩展文件。</p></td>
<td><p>无。</p></td>
<td><p>BidiWSDFile =FABidiWSD.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>BidiUSBFile</strong></p>
<p>这会为 USB 定义双向扩展。</p></td>
<td><p>无。</p></td>
<td><p>BidiUSBFile =FABidiUSB.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBJSFile</strong></p>
<p>这会定义用于 USB 的 JavaScript 扩展。</p></td>
<td><p>无。</p></td>
<td><p>BidiUSBJSFile =FABidiUSBJS.js</p></td>
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
<th>使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PageOutputQuality.OptionName</strong></p>
<p>基于 PageOutputQuality 的作业 PrintTicket 中的值更改图像压缩</p></td>
<td><p>OptionName 必须是标准 PrintSchema 命名空间中指定的名称。</p></td>
<td><p>PageOutputQuality =</p>
<p>MxdcImageType.JPEGHigh</p>
<p>PageOutputQuality =</p>
<p>MxdcImageType.JPEGMedium</p>
<p>PageOutputQuality =</p>
<p>MxdcImageType.PNG</p></td>
</tr>
<tr class="even">
<td><p><strong>XpsFormat</strong></p>
<p>更改此驱动程序的打印系统生成的 XPS 格式。 可以指定多个值，顺序代表驱动程序的首选项。</p></td>
<td><p>不能用于使用 Unidrv/PScript 呈现的类驱动程序。</p></td>
<td><p>XpsFormat = XPS</p>
<p>XpsFormat = OpenXPS</p>
<p>XPSFormat = OpenXPS，XPS</p>
<p>XPSFormat = XPS，OpenXPS</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputFormat</strong></p>
<p>OutputFormat 指令描述了使用 MIME 类型由此驱动程序生成的单个 PDL。</p>
<p>此信息将在 WSD 打印机的 Batchclient.joboperations.createjob 或 CreateJob2 操作过程中使用。</p></td>
<td><p>无。</p></td>
<td><p>有效的使用类型包括：</p>
<p>OutputFormat =</p>
<p>"application/.oxps"</p>
<p>OutputFormat =</p>
<p>"application/vnd.apple.mpegurl. ms-xpsdocument"</p>
<p>OutputFormat =</p>
<p>"image/pwg"</p>
<p>OutputFormat =</p>
<p>"application/vnd.apple.mpegurl. ms-3mfdocument"</p>
<p>还可以在此处指定任何其他有效的已定义 MIME 类型。</p></td>
</tr>
</tbody>
</table>

 

PageOutputQuality 指令的 MxdcImageType 关键字具有以下允许值：

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
<p>高压缩 JPEG (小型文件) </p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.JPEGMedium</strong></p>
<p>中等压缩 JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGLow</strong></p>
<p>低压缩 JPEG</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.PNG</strong></p>
<p>PNG 文件类型 (最大的文件) </p></td>
</tr>
</tbody>
</table>

 

## <a name="filesave-section"></a>FileSave 部分


本部分支持文件保存方案。 为新的 PORTPROMPT 端口类型安装 v4 打印驱动程序时，此部分指定要在 " **公共文件** " 窗口中显示的文件扩展名，还指定支持扩展和对话框本身的可本地化资源字符串。

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
<th>使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>&lt;FileExtensionName&gt;</strong></p>
<p>此指令介绍使用 PORTPROMPT 端口保存此驱动程序中的文件时使用的 FileExtension。 该值是驱动程序的 ResourceFile 中的 resourceID。 对于 XPS 和 .OXPS，可以指定 Id 为0的 resourceID，打印后台处理程序将使用其内部资源。</p></td>
<td><p>无。</p></td>
<td><p>&lt;FileExtensionName&gt;=</p>
<p>&lt;resourceID&gt;</p>
<p>Xps = 1234</p></td>
</tr>
<tr class="even">
<td><p><strong>SaveAsTitle</strong></p>
<p>此指令描述要在 "保存文件" 对话框中使用的标题。 该值是驱动程序的 ResourceFile 中的 resourceID。</p></td>
<td><p>无。</p></td>
<td><p>SaveAsTitle =</p>
<p>&lt;resourceID&gt;</p>
<p>SaveAsTitle =</p>
<p>4321</p></td>
</tr>
</tbody>
</table>

 

## <a name="printerextensions-section"></a>PrinterExtensions 部分


PrinterExtensions 节指定打印机扩展和它支持的调用模式。 对于这两个条目，应用将自动注册到打印系统。 此外，应用将以该顺序配置两个不同的参数，即 PrinterDriverID 和 ReasonID。 因此，每个条目必须使用不同的 PrinterExtensionID GUID。

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
<th>使用情况</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DriverEvent</strong></p>
<p>用于维护 DriverEvent 模式的应用。</p></td>
<td><p>无。</p></td>
<td><p>DriverEvent =</p>
<p>app.exe {extensionID GUID}</p></td>
</tr>
<tr class="even">
<td><p><strong>PrintPreferences</strong></p>
<p>用于维护 PrintPreferences 模式的应用。</p></td>
<td><p>无。</p></td>
<td><p>PrintPreferences =</p>
<p>app.exe {extensionID GUID}</p></td>
</tr>
</tbody>
</table>

 

下面是 v4 打印驱动程序清单的示例。

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
PrinterExtensionUrl="https://www.fabrikam.com/download.asp?uiapp=120"
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
[打印机 INF 文件项](printer-inf-file-entries.md)  



