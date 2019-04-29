---
Description: 对功能命令 （WpdServiceSampleDriver 示例） 的支持
title: 对功能命令 （WpdServiceSampleDriver 示例） 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3125c92465bc90d9f60816239ca6ed3301ed1dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370486"
---
# <a name="support-for-capability-commands-wpdservicesampledriver-sample"></a>对功能命令 （WpdServiceSampleDriver 示例） 的支持


示例驱动程序支持的服务的设备的十个功能命令和 14 功能命令。 支持的设备功能命令的代码中找到*WpdCapabilities.cpp*。 支持的服务功能命令的代码中找到*WpdServiceCapabilities.cpp*。 WPD 调用这些命令时应用程序中检索设备功能或服务功能的数据。 例如，当应用程序调用**IPortableDeviceServiceCapabilities::GetSupportedFormats**，WPD 发出相应 WPD\_命令\_服务\_功能\_获取\_支持\_格式命令向驱动程序检索给定的服务支持的格式。

## <a name="span-idthedevice-capabilitycommandsspanspan-idthedevice-capabilitycommandsspanspan-idthedevice-capabilitycommandsspanthe-device-capability-commands"></a><span id="The_Device-Capability_Commands"></span><span id="the_device-capability_commands"></span><span id="THE_DEVICE-CAPABILITY_COMMANDS"></span>设备功能命令


当应用程序调用中的几种方法之一发布设备功能命令**IPortableDeviceCapabilities**接口。 这些命令处理最初由**WpdCapabilities::DispatchMessage**反过来，将调用相应的命令处理程序的方法。 **DispatchMessage**方法和单个处理程序中找到*WpdCapabilities.cpp*文件。下表描述了每个设备功能命令处理程序的名称以及该**DispatchMessage**处理给定的命令时调用。

| Command                                                            | 处理程序                        | 描述                                                                                                                                  |
|--------------------------------------------------------------------|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| WPD\_命令\_功能\_获取\_支持\_命令               | OnGetSupportedCommands         | 应用程序尝试检索的设备支持的命令集时，发出。                                           |
| WPD\_命令\_功能\_获取\_命令\_选项                  | OnGetCommandOptions            | 应用程序尝试检索受给定命令的选项时，发出。                                              |
| WPD\_命令\_功能\_获取\_支持\_功能\_类别 | OnGetFunctionalCategories      | 应用程序尝试检索的设备支持的功能类别组时，发出。                              |
| WPD\_命令\_功能\_获取\_功能\_对象               | OnGetFunctionalObjects         | 应用程序尝试检索受给定功能分类的函数对象的组时，发出。                |
| WPD\_命令\_功能\_获取\_支持\_内容\_类型         | OnGetSupportedContentTypes     | 应用程序尝试检索给定功能分类支持的内容类型时，发出。                            |
| WPD\_命令\_功能\_获取\_支持\_格式                | OnGetSupportedFormats          | 当应用程序尝试检索组的支持给定的内容类型的格式时发出。                                  |
| WPD\_命令\_功能\_获取\_支持\_格式\_属性     | OnGetSupportedFormatProperties | 应用程序尝试检索给定格式支持的属性集时，发出。                                     |
| WPD\_命令\_功能\_获取\_FIXED\_属性\_属性       | OnGetFixedPropertyAttributes   | 当应用程序尝试检索的属性完全相同 （或固定） 的属性集时，发出针对给定格式的所有对象。 |
| WPD\_命令\_功能\_获取\_事件\_选项                    | OnGetEventOptions              | 应用程序尝试检索与给定的事件相关联的选项时，发出。                                             |
| WPD\_命令\_功能\_获取\_支持\_事件                 | OnGetSupportedEvents           | 当应用程序尝试检索一组支持的设备的事件时发出。                                               |

 

## <a name="span-idtheservice-capabilitycommandsspanspan-idtheservice-capabilitycommandsspanspan-idtheservice-capabilitycommandsspanthe-service-capability-commands"></a><span id="The_Service-Capability_Commands"></span><span id="the_service-capability_commands"></span><span id="THE_SERVICE-CAPABILITY_COMMANDS"></span>服务功能命令


当应用程序调用中的几种方法之一，在发出服务功能命令**IPortableDeviceServiceCapabilities**接口。 这些命令处理最初由**WpdServiceCapabilities::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序中找到*WpdServiceCapabilities.cpp*文件。下表描述了每个设备功能命令处理程序的名称以及该**DispatchMessage**处理给定的命令时调用。

| Command                                                                     | 处理程序                        | 描述                                                                                                            |
|-----------------------------------------------------------------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| WPD\_命令\_服务\_功能\_获取\_支持\_命令               | OnGetSupportedCommands         | 应用程序尝试检索给定的服务支持的命令集时，发出。              |
| WPD\_命令\_服务\_功能\_获取\_命令\_选项                  | OnGetCommandOptions            | 应用程序尝试检索受给定命令的选项时，发出。                        |
| WPD\_命令\_服务\_功能\_获取\_支持\_方法                | OnGetSupportedMethods          | 当应用程序尝试检索给定的服务支持的方法时发出。                      |
| WPD\_命令\_服务\_功能\_获取\_支持\_方法\_BY\_格式    | OnGetSupportedMethodsByFormat  | 当应用程序尝试检索在给定服务上以给定格式支持的方法时发出。    |
| WPD\_命令\_服务\_功能\_获取\_方法\_属性                | OnGetMethodAttributes          | 应用程序尝试检索给定方法的属性时，发出。                                        |
| WPD\_命令\_服务\_功能\_获取\_方法\_参数\_属性     | OnGetMethodParameterAttributes | 应用程序尝试检索给定的方法参数的属性时，发出。                              |
| WPD\_命令\_服务\_功能\_获取\_支持\_功能\_类别 | OnGetFunctionalCategories      | 当应用程序尝试检索的一组给定的服务支持的功能类别时发出。 |
| WPD\_命令\_服务\_功能\_获取\_支持\_格式                | OnGetSupportedFormats          | 当应用程序尝试检索给定服务支持的格式时发出。                        |
| WPD\_命令\_服务\_功能\_获取\_格式\_属性                | OnGetFormatAttributes          | 应用程序尝试检索服务支持以给定格式的属性时，发出。        |
| WPD\_命令\_服务\_功能\_获取\_支持\_格式\_属性     | OnGetSupportedFormatProperties | 应用程序尝试检索给定格式支持的属性集时，发出。               |
| WPD\_命令\_服务\_功能\_获取\_格式\_属性\_属性      | OnGetFormatPropertyAttributes  | 应用程序尝试检索在服务上以给定格式的属性特性的组时，发出。         |
| WPD\_命令\_服务\_功能\_获取\_支持\_事件                 | OnGetSupportedEvents           | 当应用程序尝试检索给定服务支持的事件时发出。                       |
| WPD\_命令\_服务\_功能\_获取\_事件\_属性                 | OnGetEventAttributes           | 应用程序尝试检索在服务上的给定事件的属性时，发出。                          |
| WPD\_命令\_服务\_功能\_获取\_事件\_参数\_属性      | OnGetEventParameterAttributes  | 应用程序尝试检索在服务上的给定事件的参数属性时，发出。                |
| WPD\_命令\_服务\_功能\_获取\_继承\_服务               | OnGetInheritedServices         | 应用程序尝试检索给定服务由继承的服务时，发出。                     |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





