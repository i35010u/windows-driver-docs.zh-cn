---
title: UVC 扩展单元的示例注册表项
description: UVC 扩展单元的示例注册表项
ms.assetid: a34e00e2-90f0-4073-8740-7f3e04d68639
keywords:
- 注册表 WDK USB 视频类
- 扩展单位 WDK USB 视频类，示例、 注册表项
- 示例代码 WDK USB 视频类，UVC 扩展单位的注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48044c0d53220ad3213b304352b19bb68f9ddb19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389210"
---
# <a name="sample-registry-entry-for-uvc-extension-units"></a>UVC 扩展单元的示例注册表项

本主题包含了可用于支持扩展单位的示例注册表项。

必须将条目添加到**HKLM\\系统\\CurrentControlSet\\控制\\NodeInterfaces**注册表子项。 此注册表子项包含属性集 GUID 值和对应于该属性集的接口的 IID 和 CLSID 值。

验证：

- 属性集 GUID 与中的 GUID 匹配[扩展单元描述符](sample-extension-unit-descriptor.md)。

- 中的 IID 和 CLSID 值**NodeInterfaces**子项存储在二进制、 小字节序窗体中。

因此，{12345678-1234年-5678-0123456789abcdef} 的 IID 值将存储为：

```cpp
78 56 34 12 34 12 78 56 01 23 45 67 89 ab cd ef
```

- Guid 必须是唯一的应由使用生成*Guidgen.exe*，Microsoft Windows SDK 中包含的工具。

在任意名为的注册表脚本中包含以下代码*Xusample.rgs*:

```cpp
HKLM
{
    NoRemove SYSTEM
    {
        NoRemove CurrentControlSet
        {
            NoRemove Control
            {
                NoRemove NodeInterfaces
                {
                    ForceRemove {xxxxxxxx-xxxx-xxxx-xxxx-
                       xxxxxxxxxxxx} = s 'Extension Unit
                       Property Set'
                    {
                        val IID = b 'yyyyyyyyyyyyyyyyyyy
                           yyyyyyyyyyyyy'
                        val CLSID = b 'zzzzzzzzzzzzzzzzz
                           zzzzzzzzzzzzzzz'
                    }
                }
            }
        }
    }
}
```

若要通过注册插件 DLL 支持安装，请向注册表脚本添加以下代码：

```cpp
HKCR
{
    NoRemove CLSID
    {
         ForceRemove {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} = s 'CompanyName Extension Unit Interface'
        {
            InprocServer32 = s '%MODULE%'
                                                {
                                val ThreadingModel = s 'Both'
                                                }
        }

    }
}
```
