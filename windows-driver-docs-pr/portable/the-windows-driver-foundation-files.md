---
description: Windows 驱动程序框架文件
title: Windows 驱动程序框架文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fef31c9a99bf4a3a1ab820c1c8e43ea9b4eb269
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969454"
---
# <a name="the-windows-driver-frameworks-files"></a>Windows 驱动程序框架文件


WpdHelloWorldDriver 项目包含以下 Windows 用户模式驱动程序框架 (UMDF) 文件。

| Filename   | 描述                                                                                                                                                                   |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备 .cpp | 包含 CDevice 成员函数的实现。 这些函数处理即插即用和电源管理事件。                                                 |
| 设备。h   | 包含 CDevice 类的定义。                                                                                                                                  |
| 驱动程序 .cpp | 包含 CDriver 成员函数的实现。 这些函数将处理设备初始化和清理。                                                         |
| 驱动程序。h   | 包含 CDriver 类的定义。                                                                                                                                  |
| Queue  | 包含 CQueue 成员函数的实现。                                                                                                                    |
| Queue。h    | 包含 CQueue 类的定义，以及 Windows Driver Foundation (WDF) 回调的定义。 这些函数将处理设备控制和文件创建。 |

 

 

 




