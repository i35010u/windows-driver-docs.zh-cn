---
Description: Supporting the Service Commands
title: 支持服务命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27fba5e4e3e40acfd1fb9a82ea930678f248972c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534011"
---
# <a name="supporting-the-service-commands"></a>支持服务命令


WPD 发出服务命令，当应用程序调用 WPD API 支持的服务接口中找到的几种方法。

在示例驱动程序，这些服务命令将首先在处理由**WpdService::DispatchMessage**方法。 此方法检查给定的命令，并将其转发到相应的处理程序。 示例驱动程序将转发到中的处理程序的功能命令的任何*WpdServiceCapabilities.cpp*模块。 示例驱动程序将转发到中的处理程序方法命令的任何*WpdServiceMethods.cpp*模块。

下表介绍了支持的服务模块，其说明和处理程序的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">说明/处理程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_START_INVOKE</td>
<td align="left"><p>说明：当应用程序调用可以颁发<strong>IPortableDeviceServiceMethods::Invoke</strong>或<strong>IPortableDeviceServiceMethods::InvokeAsync</strong>方法。</p>
<p>Handler:<strong>WpdServiceMethods::OnStartInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_METHODS_END_INVOKE</td>
<td align="left"><p>说明：由应用程序调用的方法运行完毕时，发出。 （WPD 发出此命令，为同步和异步方法。）</p>
<p>处理程序：<strong>WpdServiceMethods::OnEndInvoke</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_CANCEL_INVOKE</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceMethods::Cancel</strong>方法来取消未完成的方法调用。</p>
<p>处理程序：<strong>WpdServiceMethods::OnCancelInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_COMMON_GET_SERVICE_OBJECT_ID</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceService::GetServiceObjectId</strong>方法来检索当前服务的对象标识符。</p>
<p>处理程序：<strong>OnGetServiceObjectID</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupportingtheservice-capabilitycommandsspanspan-idsupportingtheservice-capabilitycommandsspanspan-idsupportingtheservice-capabilitycommandsspansupporting-the-service-capability-commands"></a><span id="Supporting_the_Service-Capability_Commands"></span><span id="supporting_the_service-capability_commands"></span><span id="SUPPORTING_THE_SERVICE-CAPABILITY_COMMANDS"></span>支持的服务功能的命令


WPD 应用程序使用的方法中找到**IPortableDeviceServiceCapabilities**界面来发现服务提供的功能。 通过此界面中使用的方法，应用程序可以检索受支持的方法、 事件和格式的说明。 并且，应用程序可以检索更多特定数据，例如给定方法的特定参数的属性。

中的示例驱动程序中， **WpdService::DispatchMessage**方法将检查**fmtid**字段的所有传入的命令。 如果此字段设置为 WPD\_类别\_服务\_功能，它将转发到命令**WpdServiceCapabilities::DispatchWpdMessage**方法，反过来，处理该命令。 ( **WpdServiceCapabilities::DispatchWpdMessage**中找到方法*WpdServiceCapabilities.cpp*文件。)

下表描述了支持的 14 功能命令**WpdServiceCapabilities::DispatchWpdMessage**方法，其说明和处理程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">说明/处理程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_COMMANDS</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedCommands</strong>来检索当前服务支持的 WPD 命令的列表。</p>
<p>处理程序：<strong>OnGetSupportedCommands</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_COMMAND_OPTIONS</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetCommandOptions</strong>检索由当前服务实现任何 WPD 命令选项。</p>
<p>处理程序：<strong>OnGetCommandOptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedMethods</strong>来检索应用于当前服务对象格式的受支持的设备服务方法的列表。</p>
<p>处理程序：<strong>OnGetSupportedMethods</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS_BY_FORMAT</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedMethodsByFormat</strong>来检索应用于当前服务对象格式的受支持的设备服务方法的列表。</p>
<p>处理程序：<strong>OnGetSupportedMethodsByFormat</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetMethodAttributes</strong>检索设备服务方法的属性 （例如，名称和参数）。</p>
<p>处理程序：<strong>OnGetMethodAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetMethodParameterAttributes</strong>检索给定的设备服务方法的参数属性 （例如，名称和 VARTYPE）。</p>
<p>处理程序：<strong>OnGetMethodParameterAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMATS</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedFormats</strong>检索受支持的对象格式以获得当前的服务。</p>
<p>处理程序：<strong>OnGetSupportedFormats</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetFormatAttributes</strong>方法。</p>
<p>处理程序：<strong>OnGetFormatAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedFormatProperties</strong>来检索给定格式受支持的属性的列表。</p>
<p>处理程序：<strong>OnGetSupportedFormatProperties</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_PROPERTY_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetFormatPropertyAttributes</strong>检索属性的属性 （例如，名称、 窗体，VARTYPE）。</p>
<p>处理程序：<strong>OnGetFormatPropertyAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_EVENTS</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetSupportedEvents</strong>来检索当前服务的支持事件的列表。</p>
<p>处理程序：<strong>OnGetSupportedEvents</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetEventAttributes</strong>检索设备服务事件的属性 （例如，名称、 参数）。</p>
<p>处理程序：<strong>OnGetEventAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetEventParameterAttributes</strong>检索给定的事件参数的属性。</p>
<p>处理程序：<strong>OnGetEventParameterAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_INHERITED_SERVICES</td>
<td align="left"><p>说明：当应用程序调用时，发出<strong>IPortableDeviceServiceCapabilities::GetInheritedServices</strong>获取由当前服务实现的抽象服务。</p>
<p>处理程序：<strong>OnGetInheritedServices</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupportingthewpdcommandservicemethodsstartinvokecommandspanspan-idsupportingthewpdcommandservicemethodsstartinvokecommandspanspan-idsupportingthewpdcommandservicemethodsstartinvokecommandspansupporting-the-wpdcommandservicemethodsstartinvoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_start_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_COMMAND"></span>支持 WPD\_命令\_服务\_方法\_启动\_INVOKE 命令


WPD 应用程序调用的方法的调用中找到的两种方法之一给定服务受**IPortableDeviceServiceMethods**接口。 **IPortableDeviceServiceMethods::Invoke**方法将调用方法，以同步方式同时**IPortableDeviceServiceMethods::InvokeAsync**方法以异步方式调用给定的方法。

WPD API 中，当应用程序调用这两种方法之一时，反过来，发出 WPD\_命令\_服务\_方法\_启动\_INVOKE 命令向驱动程序。

中的示例驱动程序，WPD\_命令\_服务\_方法\_启动\_INVOKE 命令结果在以下表中，可在方法调用*WpdServiceMethods.cpp*模块。

| 方法名称                          | 描述                                                                                                                                                                                                           |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnStartInvoke** | 调用**StartMethod**帮助器函数完成后，返回调用的方法的上下文中并**IPortableDeviceValues**对象。                                                                           |
| **WpdServiceMethods::StartMethod**   | 验证给定的服务支持所请求的方法，以及如果是这样，创建一个新**ServiceMethodContext**对象。 创建上下文后， **ServiceMethodContext::Initalize**调用方法。 |
| **ServiceMethodContext::Initialize** | 创建**CMethodTask**对象，并调用**CMethodTask::Run**方法。                                                                                                                                         |
| **CMethodTask::Run**                 | 创建一个单独的线程调用的方法可以在其中运行。                                                                                                                                                        |

 

当**WpdServiceMethods::OnStartInvoke**方法调用，WPD 传递正在调用的方法的 GUID 标识符。 向该数据传递此 GUID *pParams*参数点。

在中找到的受支持的方法的 Guid *ContactDeviceService.h*并*FullEnumSyncDeviceService.h*标头文件。

方法上下文是一个字符串，该驱动程序和 WPD 用于标识且针对给定的方法的调用。 例如，WPD 发出命令以取消给定方法的特定调用，或以指示该方法完成时，使用此字符串。

## <a name="span-idsupportingthewpdcommandservicemethodsendinvokecommandspanspan-idsupportingthewpdcommandservicemethodsendinvokecommandspanspan-idsupportingthewpdcommandservicemethodsendinvokecommandspansupporting-the-wpdcommandservicemethodsendinvoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_end_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_COMMAND"></span>支持 WPD\_命令\_服务\_方法\_最终\_INVOKE 命令


方法完成时，驱动程序将发送 WPD\_事件\_服务\_WPD api 完成事件。 事件数据包括驱动程序时调用该方法创建的方法上下文。 WPD API 收到此事件通知时，发出 WPD\_命令\_服务\_方法\_最终\_调用命令，并包括使用此命令的方法上下文。 当示例驱动程序收到此命令时，这会导致中找到的以下方法调用*WpdServiceMethods.cpp*。

| 方法名称                        | 描述                                                                                                                                                                                                                   |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnEndInvoke** | 调用**EndMethod**帮助器函数和完成后，返回调用的方法的结果和状态代码。 此方法还会清理的任何必要的资源所带来的方法上下文执行。 |
| **WpdServiceMethods::EndMethod**   | 检索调用的方法的结果和状态代码...                                                                                                                                                                      |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[The WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





