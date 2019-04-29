---
Description: COM 组件文件
title: COM 组件文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17655c0df198cc48e4c1c2baeccb871be84e9ffa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380839"
---
# <a name="the-com-component-files"></a>COM 组件文件


WpdHelloWorldDriver 项目包含以下 COM 组件文件。

| Filename                | 描述                                                                                                                                               |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| resource.h              | 包含单个的定义，驱动程序的标识符。                                                                                                 |
| stdafx.h                | 包括标准系统文件。                                                                                                                           |
| WpdHelloWorldDriver.cpp | 包含处理服务器注册，返回类工厂和 DLL 的入口点的基本 COM 方法。                                       |
| WpdHelloWorldDriver.def | 声明模块参数。                                                                                                                           |
| WpdHelloWorldDriver.idl | 包含驱动程序的 COM 组件的必要定义。                                                                                        |
| WpdHelloWorldDriver.rc  | 包含定义所需的驱动程序资源。 这些资源包括的文件类型、 文件描述字符串和原始文件名。 |
| WpdHelloWorldDriver.rgs | 包含驱动程序的 COM 组件注册脚本。                                                                                          |

 

 

 




