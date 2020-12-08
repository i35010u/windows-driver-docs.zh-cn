---
title: 增强的存储证书管理工具命令语法
description: 增强的存储证书管理工具通过使用不同的命令行开关来提供证书管理操作。
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
ms.openlocfilehash: b04e21e0f004274bb413191e14352d923a8868fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814499"
---
# <a name="enhanced-storage-certificate-management-tool-command-syntax"></a>增强的存储证书管理工具命令语法


增强的存储证书管理工具通过使用不同的命令行开关来提供证书管理操作。 每个开关定义自己的一组参数，例如卷名称和证书索引。

增强的存储证书管理工具是从命令行运行的。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________Add______"></span><span id="________add______"></span><span id="________ADD______"></span>**/Add**   
将证书添加到 (ASC) 存储设备1667上的身份验证接收器证书。 有关详细信息，请参阅 [**/Add 开关**](enhstor-add-switch.md)。

<span id="________Clear______"></span><span id="________clear______"></span><span id="________CLEAR______"></span>**/Clear**   
删除指定的与 IEEE 1667 兼容的 USB 存储设备上 ASC 存储区中的所有证书。 有关详细信息，请参阅 [**/Clear 开关**](-clear-switch.md)。

<span id="________Debug______"></span><span id="________debug______"></span><span id="________DEBUG______"></span>**/Debug**   
报告与 IEEE 1667 兼容 USB 存储设备中的 ASC 存储区相关的功能和信息。 有关详细信息，请参阅 [**/Debug 开关**](-debug-switch.md)。

<span id="________Export______"></span><span id="________export______"></span><span id="________EXPORT______"></span>**/Export**   
将指定的证书从符合 IEEE 1667 的 USB 存储设备中的 ASC 存储导出到文件。 此开关还支持将 (CSR) 的证书签名请求导出到文件。

有关详细信息，请参阅 [**/Export 开关**](-export-switch.md)。

<span id="________Help______"></span><span id="________help______"></span><span id="________HELP______"></span>**/Help**   
显示有关增强的存储证书管理工具的使用情况信息。 通过使用 **/？** ，可以显示相同的帮助信息。 转.

<span id="________Initialize______"></span><span id="________initialize______"></span><span id="________INITIALIZE______"></span>**/Initialize**   
将符合 IEEE 1667 的 USB 存储设备中的 ASC 存储初始化为其原始制造商的状态。 有关详细信息，请参阅 [**/Initialize 开关**](-initialize-switch.md)。

<span id="________List______"></span><span id="________list______"></span><span id="________LIST______"></span>**/List**   
列出连接到计算机的所有符合 IEEE 1667 的 USB 存储设备。 此开关还可用于列出符合 IEEE 1667 的 USB 存储设备中 ASC 存储区中的证书。

有关详细信息，请参阅 [**/List 开关**](-list-switch.md)。

<span id="________Remove______"></span><span id="________remove______"></span><span id="________REMOVE______"></span>**/Remove**   
从符合 IEEE 1667 的 USB 存储设备中的 ASC 存储区中删除指定的证书。 有关详细信息，请参阅 [**/Remove 开关**](-remove-switch.md)。

<span id="________Replace______"></span><span id="________replace______"></span><span id="________REPLACE______"></span>**/Replace**   
从符合 IEEE 1667 的 USB 存储设备中的 ASC 存储替换指定的证书。 有关详细信息，请参阅 [**/Replace 开关**](-replace-switch.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

增强的存储证书管理工具无法添加、删除或替换基于 IEEE 1667 兼容 USB 存储设备中 ASC 存储区中的 asc 制造商 (ASCm) 证书。 有关此和其他 IEEE 1667 证书类型的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

增强的存储证书管理工具的所有交换机必须以斜杠标记 ( "/" ) 或 ( "-" ) 。 开关的参数必须以破折号开头。 开关和相关参数不区分大小写。

.









