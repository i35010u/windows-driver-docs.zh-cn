---
Description: Windows 驱动程序框架文件
title: Windows 驱动程序框架文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745b470dd602b4098587f4a3faf433c14ccff7b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378201"
---
# <a name="the-windows-driver-frameworks-files"></a>Windows 驱动程序框架文件


WpdHelloWorldDriver 项目包含以下 Windows 用户模式驱动程序框架 (UMDF) 文件。

| Filename   | 描述                                                                                                                                                                   |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Device.cpp | 包含 CDevice 成员函数的实现。 这些函数处理插和电源管理事件。                                                 |
| Device.h   | 包含 CDevice 类的定义。                                                                                                                                  |
| Driver.cpp | 包含 CDriver 成员函数的实现。 这些函数处理设备初始化和清理。                                                         |
| Driver.h   | 包含 CDriver 类的定义。                                                                                                                                  |
| Queue.cpp  | 包含 CQueue 成员函数的实现。                                                                                                                    |
| Queue.h    | 包含 CQueue 类的定义以及 Windows Driver Foundation (WDF) 回调的定义。 这些函数处理控件和文件创建设备。 |

 

 

 




