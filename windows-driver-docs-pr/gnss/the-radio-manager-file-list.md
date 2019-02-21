---
title: 单选 manager 文件列表
description: 下表描述在单选管理器 DLL 中找到的文件。
ms.assetid: 70A8B11F-89FF-49E3-933E-2BB66D5E1BF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e3ca5785a317105ef72ccd189af999e9b1d15f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543506"
---
# <a name="the-radio-manager-file-list"></a>单选 manager 文件列表

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

下表描述在单选管理器 DLL 中找到的文件。

|                              |                                                                                                                                                                                                                                             |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 文件名                    | 目录                                                                                                                                                                                                                                    |
| SampleRM.sln                 | 生成示例单选管理器 dll 的 Visual Studio 2010 解决方案文件                                                                                                                                                              |
| sampleRM.idl                 | 接口定义的示例单选管理器                                                                                                                                                                                       |
| RadioMgr.idl                 | 接口定义为 Windows 单选管理器                                                                                                                                                                                        |
| SampleRadioManager.h         | 头文件所需为单选管理器的功能。                                                                                                                                                                                  |
| SampleRadioInstance.h        | 对于单选实例所需的功能的标头文件                                                                                                                                                                                 |
| SampleInstanceCollection.h   | 对于单选实例集合所需的功能的标头文件                                                                                                                                                                  |
| precomp.h                    | 常见头文件                                                                                                                                                                                                                          |
| dllmain.cpp                  | 标准 dllmain                                                                                                                                                                                                                            |
| InternalInterfaces.h         | 此示例使用的内部接口的标头文件                                                                                                                                                                                     |
| SampleRadioManager.cpp       | 实现详细信息的示例单选管理器。 重要的概念包括:-利用 IMediaRadioManagerNotifySink 单选实例事件-添加/删除单选实例的队列和部署系统事件的辅助角色作业 |
| SampleRadioInstance.cpp      | 示例单选实例的实现细节。 重要的概念包括： 访问器 （& m) 无线电收发器信息的修饰符的实例更改函数                                                                                 |
| SampleInstanceCollection.cpp | 示例实例集合的实现细节。 重要的概念包括:-单选实例发现和检索                                                                                                             |
| RadioMgr\_interface.cpp      | 帮助程序源文件以包含 MIDL 生成的文件。                                                                                                                                                                                     |

 

 

 




