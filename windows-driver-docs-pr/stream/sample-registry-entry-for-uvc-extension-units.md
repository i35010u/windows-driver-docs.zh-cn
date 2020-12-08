---
title: UVC 扩展单元的示例注册表项
description: UVC 扩展单元的示例注册表项
keywords:
- 注册表 WDK USB 视频类
- 扩展单元-WDK USB 视频类、示例、注册表项
- 示例代码 WDK USB 视频类，UVC 扩展单元的注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe066a0bd307c8ccbd3d77120a43412b241761cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806631"
---
# <a name="sample-registry-entry-for-uvc-extension-units"></a>UVC 扩展单元的示例注册表项

本主题包含可用于支持扩展单元的示例注册表项。

必须将这些项添加到 **HKLM \\ System \\ CurrentControlSet \\ Control \\ NodeInterfaces** 注册表子项。 此注册表子项包含属性集 GUID 值以及对应于该属性集的接口的 IID 和 CLSID 值。

验证：

- 属性集 GUID 与 [扩展单元描述符](sample-extension-unit-descriptor.md)中的 guid 匹配。

- **NodeInterfaces** 子项中的 IID 和 CLSID 值以二进制的小字节序形式存储。

因此，将 {12345678-1234-5678-0123456789abcdef} 的 IID 值存储为：

```cpp
78 56 34 12 34 12 78 56 01 23 45 67 89 ab cd ef
```

- Guid 必须唯一，并且应使用 *Guidgen.exe*（包含在 Microsoft Windows SDK 中的工具）生成。

将以下代码包含在注册表脚本中（任意名为 *Xusample*）：

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

若要通过注册插件 DLL 来支持安装，请将以下代码添加到注册表脚本：

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
