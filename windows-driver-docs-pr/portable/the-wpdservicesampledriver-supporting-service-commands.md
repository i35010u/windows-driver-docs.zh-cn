---
description: 支持服务命令
title: 支持服务命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb0c439ff2abb825e57aa4347c44dddec26e2e0
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969398"
---
# <a name="supporting-the-service-commands"></a>支持服务命令


当应用程序调用在 WPD API 支持的服务接口中找到的多个方法时，WPD 会发出服务命令。

在示例驱动程序中，将首先通过 **WpdService：:D ispatchmessage** 方法处理这些服务命令。 此方法检查给定的命令，并将其转发到相应的处理程序。 示例驱动程序将任何功能命令转发到 *WpdServiceCapabilities* 模块中的处理程序。 示例驱动程序将任何方法命令转发到 *WpdServiceMethods* 模块中的处理程序。

下表描述了服务模块支持的命令及其说明和处理程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">Description/处理程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_START_INVOKE</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceMethods：： Invoke</strong> 或 <strong>IPortableDeviceServiceMethods：： InvokeAsync</strong> 方法时发出。</p>
<p>处理程序：<strong>WpdServiceMethods：： OnStartInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_METHODS_END_INVOKE</td>
<td align="left"><p>说明：在应用程序调用的方法运行完毕后发出。  (WPD 为同步和异步方法发出此命令。 ) </p>
<p>处理程序： <strong>WpdServiceMethods：： OnEndInvoke</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_METHODS_CANCEL_INVOKE</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceMethods：： cancel</strong> 方法来取消尚未完成的方法调用时发出。</p>
<p>处理程序： <strong>WpdServiceMethods：： OnCancelInvoke</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_COMMON_GET_SERVICE_OBJECT_ID</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceService：： GetServiceObjectId</strong> 方法检索当前服务的对象标识符时发出。</p>
<p>处理程序： <strong>OnGetServiceObjectID</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupporting_the_service-capability_commandsspanspan-idsupporting_the_service-capability_commandsspanspan-idsupporting_the_service-capability_commandsspansupporting-the-service-capability-commands"></a><span id="Supporting_the_Service-Capability_Commands"></span><span id="supporting_the_service-capability_commands"></span><span id="SUPPORTING_THE_SERVICE-CAPABILITY_COMMANDS"></span>支持服务功能命令


WPD 应用程序使用 **IPortableDeviceServiceCapabilities** 接口中的方法来发现服务提供的功能。 通过使用此接口中的方法，应用程序可以检索受支持的方法、事件和格式的说明。 而且，应用程序可以检索更具体的数据，例如给定方法的特定参数的属性。

在示例驱动程序中， **WpdService：:D ispatchmessage** 方法将检查所有传入命令的 **fmtid** 字段。 如果此字段设置为 WPD \_ 类别 \_ 服务 \_ 功能，则会将命令转发到 **WpdServiceCapabilities：:D ispatchwpdmessage** 方法，该方法反过来会处理该命令。  (在*WpdServiceCapabilities*文件中找到**WpdServiceCapabilities：:D ispatchwpdmessage**方法。 ) 

下表介绍了 **WpdServiceCapabilities：:D ispatchwpdmessage** 方法支持的14种功能命令，以及它们的说明和处理程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">Description/处理程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_COMMANDS</td>
<td align="left"><p>说明：当应用程序调用<strong>IPortableDeviceServiceCapabilities：： GetSupportedCommands</strong> 检索当前服务支持的 WPD 命令的列表时发出。</p>
<p>处理程序： <strong>OnGetSupportedCommands</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_COMMAND_OPTIONS</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetCommandOptions</strong> 来检索由当前服务实现的任何 WPD 命令选项时发出。</p>
<p>处理程序： <strong>OnGetCommandOptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetSupportedMethods</strong> 来检索适用于当前服务的对象格式的受支持设备服务方法的列表时发出。</p>
<p>处理程序： <strong>OnGetSupportedMethods</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_METHODS_BY_FORMAT</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetSupportedMethodsByFormat</strong> 来检索适用于当前服务的对象格式的受支持设备服务方法的列表时发出。</p>
<p>处理程序： <strong>OnGetSupportedMethodsByFormat</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetMethodAttributes</strong> 检索特性 (例如，) 设备服务方法的名称和参数时发出。</p>
<p>处理程序： <strong>OnGetMethodAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_METHOD_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetMethodParameterAttributes</strong> 检索参数特性 (例如，指定设备服务方法的 NAME 和 VARTYPE) 时发出。</p>
<p>处理程序： <strong>OnGetMethodParameterAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMATS</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetSupportedFormats</strong> 检索当前服务支持的对象格式时发出。</p>
<p>处理程序： <strong>OnGetSupportedFormats</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_ATTRIBUTES</td>
<td align="left"><p>说明：应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetFormatAttributes</strong> 方法时发出。</p>
<p>处理程序： <strong>OnGetFormatAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetSupportedFormatProperties</strong> 检索给定格式支持的属性列表时发出。</p>
<p>处理程序： <strong>OnGetSupportedFormatProperties</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_FORMAT_PROPERTY_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetFormatPropertyAttributes</strong> 检索特性 (例如，name、FORM、VARTYPE) 属性时发出。</p>
<p>处理程序： <strong>OnGetFormatPropertyAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_SUPPORTED_EVENTS</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetSupportedEvents</strong> 检索当前服务支持的事件列表时发出。</p>
<p>处理程序： <strong>OnGetSupportedEvents</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_ATTRIBUTES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetEventAttributes</strong> 检索特性 (例如，名称、参数) 设备服务事件时发出。</p>
<p>处理程序： <strong>OnGetEventAttributes</strong></p></td>
</tr>
<tr class="odd">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_EVENT_PARAMETER_ATTRIBUTES</td>
<td align="left"><p>说明：应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetEventParameterAttributes</strong> 检索给定事件参数的属性时发出。</p>
<p>处理程序： <strong>OnGetEventParameterAttributes</strong></p></td>
</tr>
<tr class="even">
<td align="left">WPD_COMMAND_SERVICE_CAPABILITIES_GET_INHERITED_SERVICES</td>
<td align="left"><p>说明：当应用程序调用 <strong>IPortableDeviceServiceCapabilities：： GetInheritedServices</strong> 以获取当前服务实现的抽象服务时发出。</p>
<p>处理程序： <strong>OnGetInheritedServices</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsupporting_the_wpd_command_service_methods_start_invoke_commandspanspan-idsupporting_the_wpd_command_service_methods_start_invoke_commandspanspan-idsupporting_the_wpd_command_service_methods_start_invoke_commandspansupporting-the-wpd_command_service_methods_start_invoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_start_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_START_INVOKE_COMMAND"></span>支持 WPD \_ 命令 \_ 服务 \_ 方法 \_ 启动 \_ INVOKE 命令


WPD 应用程序通过调用 **IPortableDeviceServiceMethods** 接口中找到的两种方法之一来调用给定服务支持的方法。 **IPortableDeviceServiceMethods：： Invoke**方法同步调用方法，而**IPortableDeviceServiceMethods：： InvokeAsync**方法以异步方式调用给定方法。

当应用程序调用这两种方法中的任一方法时，WPD API 将发出 WPD \_ 命令 \_ 服务方法 \_ ， \_ \_ 并向驱动程序启动调用命令。

在示例驱动程序中，WPD \_ 命令 \_ 服务 \_ 方法 \_ 启动 \_ 调用命令以调用下表中的方法，这些方法在 *WpdServiceMethods* 模块中。

| 方法名称                          | 说明                                                                                                                                                                                                           |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnStartInvoke** | 调用 **StartMethod** helper 函数并在完成后返回 **IPortableDeviceValues** 对象中调用的方法的上下文。                                                                           |
| **WpdServiceMethods::StartMethod**   | 验证给定的服务是否支持请求的方法，如果存在，则创建一个新的 **ServiceMethodContext** 对象。 创建上下文后，将调用 **ServiceMethodContext：：初始化** 方法。 |
| **ServiceMethodContext：： Initialize** | 创建 **CMethodTask** 对象并调用 **CMethodTask：： Run** 方法。                                                                                                                                         |
| **CMethodTask：： Run**                 | 创建一个单独的线程，调用的方法可在该线程中运行。                                                                                                                                                        |

 

调用 **WpdServiceMethods：： OnStartInvoke** 方法时，WPD 为所调用的方法传递 GUID 标识符。 此 GUID 将传入 *pParams* 参数指向的数据。

在 *ContactDeviceService* 和 *FullEnumSyncDeviceService* 标头文件中可以找到受支持的方法的 guid。

方法上下文是驱动程序和 WPD 用于标识和定位给定方法的调用的字符串。 例如，当 WPD 发出命令来取消特定方法的特定调用或通知该方法的完成时，将使用此字符串。

## <a name="span-idsupporting_the_wpd_command_service_methods_end_invoke_commandspanspan-idsupporting_the_wpd_command_service_methods_end_invoke_commandspanspan-idsupporting_the_wpd_command_service_methods_end_invoke_commandspansupporting-the-wpd_command_service_methods_end_invoke-command"></a><span id="Supporting_the_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_Command"></span><span id="supporting_the_wpd_command_service_methods_end_invoke_command"></span><span id="SUPPORTING_THE_WPD_COMMAND_SERVICE_METHODS_END_INVOKE_COMMAND"></span>支持 WPD \_ 命令 \_ 服务 \_ 方法 \_ END \_ INVOKE 命令


当方法完成时，驱动程序将 WPD \_ 事件 \_ 服务 \_ 完成事件发送到 WPD API。 事件数据包含驱动程序在调用该方法时创建的方法上下文。 收到此事件通知后，WPD API 将发出 WPD \_ 命令 \_ 服务 \_ 方法 \_ END \_ INVOKE 命令，并在此命令中包含方法上下文。 当示例驱动程序收到此命令时，将导致对 *WpdServiceMethods*中的以下方法的调用。

| 方法名称                        | 说明                                                                                                                                                                                                                   |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WpdServiceMethods::OnEndInvoke** | 调用 **EndMethod** helper 函数并在完成后返回调用方法的结果和状态代码。 此方法还对与方法上下文相关联的资源执行任何必要的清理。 |
| **WpdServiceMethods：： EndMethod**   | 检索调用的方法的结果和状态代码。                                                                                                                                                                      |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





