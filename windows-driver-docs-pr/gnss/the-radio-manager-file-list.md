---
title: 无线电管理器文件列表
description: 下表描述了在收音机管理器 DLL 中找到的文件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715b40f4ba144607f3f27ec7eb4600c2bedb6987
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815399"
---
# <a name="the-radio-manager-file-list"></a>无线电管理器文件列表

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

下表描述了在收音机管理器 DLL 中找到的文件。

**文件名**：内容

**SampleRM**：用于生成示例收音机管理器 Dll 的 Visual Studio 2010 解决方案文件

**sampleRM**：示例收音机管理器的接口定义

**RadioMgr**： Windows 收音机管理器的接口定义

**SampleRadioManager**：收音机管理器所需功能的头文件

**SampleRadioInstance**：收音机实例所需功能的头文件

**SampleInstanceCollection**：单选按钮集合所需的函数头文件

**precomp**：通用标头文件

**dllmain .cpp**：标准 dllmain

**InternalInterfaces**：用于此示例的内部接口的标头文件

**SampleRadioManager**：示例收音机管理器的实现详细信息。 重要概念包括：-利用 IMediaRadioManagerNotifySink 实现收音机实例事件-添加/删除收音机实例-为系统事件排队和部署工作作业

**SampleRadioInstance**：示例广播实例的实现详细信息。 重要概念包括：-访问器 & 用于广播信息实例更改函数的修饰符

**SampleInstanceCollection**：示例实例集合的实现详细信息。 重要概念包括：-无线电实例发现和检索

**RadioMgr \_ interface .Cpp**： Helper 源文件，其中包含 MIDL 生成的文件。


 

 

 




