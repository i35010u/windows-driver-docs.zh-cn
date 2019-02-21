---
title: 增强的存储证书管理工具命令语法
description: 增强型存储证书管理工具进行证书管理操作使用不同的命令行开关。
ms.assetid: 4b46bdac-77e3-4b73-8942-64d902d53564
keywords:
- 增强的存储证书管理工具命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- Enhanced
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42f94f56ca4a3de83a968ae72e6a78e36b75518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521610"
---
# <a name="enhanced-storage-certificate-management-tool-command-syntax"></a>增强的存储证书管理工具命令语法


增强型存储证书管理工具进行证书管理操作使用不同的命令行开关。 每个开关定义自己的参数，例如卷名称和证书索引的一组。

增强型存储证书管理工具从命令行运行。

```
    EhStorCertMgrCmd 
    [/Add 
    AddParameters 
    |  

    /Clear 
    ClearParameters
    |

    /Debug 
    DebugParameters
    |

    /Export 
    ExportParameters
    |

    /Help|/?|

    /Initialize 
    InitializeParameters

    |
    /List [
    ListParameters
]| 

    /Remove 
    RemoveParameters
    |

    /Replace 
    ReplaceParameters
    ]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________Add______"></span><span id="________add______"></span><span id="________ADD______"></span> **/ 添加**   
将证书添加到指定 IEEE 1667 合规 USB 存储设备上的身份验证接收器证书 (ASC) 存储。 有关详细信息，请参阅[**添加 Switch**](enhstor-add-switch.md)。

<span id="________Clear______"></span><span id="________clear______"></span><span id="________CLEAR______"></span> **/Clear**   
从指定 IEEE 1667 合规 USB 存储设备上的 ASC 存储区中删除所有证书。 有关详细信息，请参阅[ **/Clear 开关**](-clear-switch.md)。

<span id="________Debug______"></span><span id="________debug______"></span><span id="________DEBUG______"></span> **/ 调试**   
报告的功能和有关 IEEE 1667 合规 USB 存储设备中的 ASC 存储区的信息。 有关详细信息，请参阅[ **/Debug 开关**](-debug-switch.md)。

<span id="________Export______"></span><span id="________export______"></span><span id="________EXPORT______"></span> **/ 导出**   
从 IEEE 1667 合规 USB 存储设备中的 ASC 存储区中指定的证书导出到文件。 此开关也支持证书签名请求 (CSR) 文件的导出。

有关详细信息，请参阅[ **/Export 开关**](-export-switch.md)。

<span id="________Help______"></span><span id="________help______"></span><span id="________HELP______"></span> **/ 帮助**   
显示有关增强的存储证书管理工具的使用情况信息。 可以使用显示相同的帮助信息 **/？** 开关。

<span id="________Initialize______"></span><span id="________initialize______"></span><span id="________INITIALIZE______"></span> **/ 初始化**   
初始化 ASC 存储 IEEE 1667 合规 USB 存储设备中，为其原始制造商的状态。 有关详细信息，请参阅[ **/Initialize 交换机**](-initialize-switch.md)。

<span id="________List______"></span><span id="________list______"></span><span id="________LIST______"></span> **/List**   
列出所有 IEEE 1667 合规 USB 存储设备连接到计算机。 此外可以使用此开关来列出 IEEE 1667 合规 USB 存储设备中的 ASC 存储区中的证书。

有关详细信息，请参阅[ **/List 交换机**](-list-switch.md)。

<span id="________Remove______"></span><span id="________remove______"></span><span id="________REMOVE______"></span> **/Remove**   
从 IEEE 1667 合规 USB 存储设备中的 ASC 存储区中删除指定的证书。 有关详细信息，请参阅[ **/Remove 交换机**](-remove-switch.md)。

<span id="________Replace______"></span><span id="________replace______"></span><span id="________REPLACE______"></span> **/ 替换**   
将替换 IEEE 1667 合规 USB 存储设备中的 ASC 存储区从指定的证书。 有关详细信息，请参阅[ **/Replace 交换机**](-replace-switch.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

增强型存储证书管理工具不能添加、 删除或替换为来自 IEEE 1667 合规 USB 存储设备中的 ASC 存储区的 ASC 制造商 (ASCm) 证书。 有关此设置和其他 IEEE 1667 证书类型的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

增强型存储证书管理工具的所有交换机必须开头斜杠标记 （'/') 或短划线 (-)。 开关的参数必须以短划线字符开头。 开关和相关的参数不区分大小写。

.









