---
description: 支持 (WpdServiceSampleDriver 示例) 的功能命令
title: 支持 (WpdServiceSampleDriver 示例) 的功能命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9063f83271f1316198750de7e57c225ad21e1956
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969544"
---
# <a name="support-for-capability-commands-wpdservicesampledriver-sample"></a>支持 (WpdServiceSampleDriver 示例) 的功能命令


示例驱动程序支持10个适用于设备的功能命令和用于服务的14个功能命令。 在 *WpdCapabilities*中可找到支持设备功能命令的代码。 支持服务功能命令的代码在 *WpdServiceCapabilities*中。 当应用程序检索设备功能或服务功能数据时，WPD 将调用这些命令。 例如，当应用程序调用 **IPortableDeviceServiceCapabilities：： GetSupportedFormats**时，WPD 会发出相应的 \_ WPD \_ 命令 \_ 服务 \_ 功能 \_ "获取 \_ 对驱动程序的支持格式" 命令，以检索给定服务支持的格式。

## <a name="span-idthe_device-capability_commandsspanspan-idthe_device-capability_commandsspanspan-idthe_device-capability_commandsspanthe-device-capability-commands"></a><span id="The_Device-Capability_Commands"></span><span id="the_device-capability_commands"></span><span id="THE_DEVICE-CAPABILITY_COMMANDS"></span>设备功能命令


当应用程序调用 **IPortableDeviceCapabilities** 接口中的几种方法之一时，将发出设备功能命令。 这些命令最初由 **WpdCapabilities：:D ispatchmessage** 方法进行处理，后者随后调用相应的命令处理程序。 在*WpdCapabilities*文件中可以找到**DispatchMessage**方法和单个处理程序。下表描述了每个设备功能命令以及**DispatchMessage**在处理给定命令时调用的处理程序的名称。

| Command                                                            | Handler                        | 说明                                                                                                                                  |
|--------------------------------------------------------------------|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 命令               | OnGetSupportedCommands         | 当应用程序尝试检索设备支持的一组命令时发出。                                           |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 命令 \_ 选项                  | OnGetCommandOptions            | 当应用程序尝试检索给定命令支持的选项时发出。                                              |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 功能 \_ 类别 | OnGetFunctionalCategories      | 当应用程序尝试检索设备支持的功能类别集时发出。                              |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 功能 \_ 对象               | OnGetFunctionalObjects         | 当应用程序尝试检索给定功能类别所支持的一组功能对象时发出。                |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 内容 \_ 类型         | OnGetSupportedContentTypes     | 当应用程序尝试检索给定功能类别所支持的内容类型时发出。                            |
| WPD \_ 命令 \_ 功能 \_ 获得 \_ 支持的 \_ 格式                | OnGetSupportedFormats          | 当应用程序尝试检索给定内容类型支持的一组格式时发出。                                  |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 格式 \_ 属性     | OnGetSupportedFormatProperties | 当应用程序尝试检索给定格式支持的属性集时发出。                                     |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 固定 \_ 属性 \_ 特性       | OnGetFixedPropertyAttributes   | 当应用程序尝试检索与给定格式的所有对象 (或固定) 相同的属性属性集时发出。 |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 事件 \_ 选项                    | OnGetEventOptions              | 当应用程序尝试检索与给定事件关联的选项时发出。                                             |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 事件                 | OnGetSupportedEvents           | 当应用程序尝试检索设备支持的一组事件时发出。                                               |

 

## <a name="span-idthe_service-capability_commandsspanspan-idthe_service-capability_commandsspanspan-idthe_service-capability_commandsspanthe-service-capability-commands"></a><span id="The_Service-Capability_Commands"></span><span id="the_service-capability_commands"></span><span id="THE_SERVICE-CAPABILITY_COMMANDS"></span>服务功能命令


当应用程序调用 **IPortableDeviceServiceCapabilities** 接口中的几种方法之一时，将发出服务功能命令。 这些命令最初由 **WpdServiceCapabilities：:D ispatchmessage** 方法进行处理，该方法反过来会调用相应的命令处理程序。 在*WpdServiceCapabilities*文件中可以找到**DispatchMessage**方法和单个处理程序。下表描述了每个设备功能命令以及**DispatchMessage**在处理给定命令时调用的处理程序的名称。

| Command                                                                     | Handler                        | 说明                                                                                                            |
|-----------------------------------------------------------------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 支持的 \_ 命令               | OnGetSupportedCommands         | 当应用程序尝试检索给定服务支持的一组命令时发出。              |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 命令 \_ 选项                  | OnGetCommandOptions            | 当应用程序尝试检索给定命令支持的选项时发出。                        |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 支持的 \_ 方法                | OnGetSupportedMethods          | 当应用程序尝试检索给定服务支持的方法时发出。                      |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ \_ 按格式获取受支持 \_ \_ 的方法 \_    | OnGetSupportedMethodsByFormat  | 当应用程序尝试检索给定服务上给定格式支持的方法时发出。    |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 方法 \_ 特性                | OnGetMethodAttributes          | 当应用程序尝试检索给定方法的属性时发出。                                        |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 方法 \_ 参数 \_ 属性     | OnGetMethodParameterAttributes | 当应用程序尝试检索给定方法参数的属性时发出。                              |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 受支持的 \_ 功能 \_ 类别 | OnGetFunctionalCategories      | 当应用程序尝试检索给定服务支持的功能类别集时发出。 |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 支持的 \_ 格式                | OnGetSupportedFormats          | 当应用程序尝试检索给定服务支持的格式时发出。                        |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 格式 \_ 特性                | OnGetFormatAttributes          | 当应用程序尝试检索服务支持的给定格式的特性时发出。        |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 支持的 \_ 格式 \_ 属性     | OnGetSupportedFormatProperties | 当应用程序尝试检索给定格式支持的属性集时发出。               |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 格式 \_ 属性 \_ 特性      | OnGetFormatPropertyAttributes  | 当应用程序尝试检索服务上给定格式的属性属性集时发出。         |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 支持的 \_ 事件                 | OnGetSupportedEvents           | 当应用程序尝试检索给定服务支持的事件时发出。                       |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 事件 \_ 属性                 | OnGetEventAttributes           | 当应用程序尝试检索服务上给定事件的属性时发出。                          |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 事件 \_ 参数 \_ 属性      | OnGetEventParameterAttributes  | 当应用程序尝试检索服务上给定事件的参数特性时发出。                |
| WPD \_ 命令 \_ 服务 \_ 功能 \_ 获取 \_ 继承的 \_ 服务               | OnGetInheritedServices         | 当应用程序尝试检索给定服务继承的服务时发出。                     |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





