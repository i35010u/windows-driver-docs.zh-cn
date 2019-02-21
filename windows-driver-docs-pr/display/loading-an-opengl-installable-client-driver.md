---
title: 正在加载 OpenGL 可安装的客户端驱动程序
description: 正在加载 OpenGL 可安装的客户端驱动程序
ms.assetid: 2b244bbf-f26c-4307-a347-a29e12c6d496
keywords:
- OpenGL ICD WDK 显示
- 加载驱动程序 WDK 显示
- ICD WDK 显示
- 可安装的客户端驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338c0d0896a789b659c17d4a5a4b5c0a5941e829
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523205"
---
# <a name="loading-an-opengl-installable-client-driver"></a>正在加载 OpenGL 可安装的客户端驱动程序


OpenGL 运行时访问注册表，以确定哪个 OpenGL 可安装的客户端驱动程序 (ICD) 加载。 若要加载 OpenGL ICD，OpenGL 运行时：

-   确定名称、 版本和标志与相关联的 OpenGL ICD 通过调用[ **D3DKMTQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547100)函数和 KMTQAITYPE\_UMOPENGLINFO 值中设置**类型**的成员[ **D3DKMT\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff548203)结构*pData*参数指向。

-   检查 OpenGL ICD 的版本号， **D3DKMTQueryAdapterInfo**返回验证 OpenGL ICD 的版本。

-   通过使用 OpenGL ICD 名称加载 OpenGL ICD。

-   初始化 OpenGL ICD 函数的访问。
    **请注意**  若要获取许可证的 OpenGL ICD 开发工具包，请联系[OpenGL 问题](mailto:opengl@microsoft.com)团队。

     

若要查找的 OpenGL ICD，名称[ **D3DKMTQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547100)注册表中搜索以下项中：

```registry
HKLM/System/CurrentControlSet/Control/Class/{Adapter GUID}/0000/
```

此项也包含的名称[Microsoft Direct3D 用户模式显示驱动程序](initializing-communication-with-the-direct3d-user-mode-display-driver.md)。 此项包含为 32 位 Windows Vista 显示驱动程序在 32 位 Windows Vista 上使用的四个注册表项，适用于 32 位 Windows Vista 的四个条目显示在 64 位 Windows Vista 使用的驱动程序。 以下条目是针对 32 位 Windows Vista 显示驱动程序在 32 位 Windows Vista 使用：

<span id="UserModeDriverName"></span><span id="usermodedrivername"></span><span id="USERMODEDRIVERNAME"></span>**UserModeDriverName**  
REG\_SZ

Direct3D 用户模式显示驱动程序，即无论操作系统是否支持 OpenGL ICD Direct3D 呈现设备的操作所必需的名称。

<span id="OpenGLDriverName"></span><span id="opengldrivername"></span><span id="OPENGLDRIVERNAME"></span>**OpenGLDriverName**  
REG\_SZ

OpenGL ICD 的名称。 例如，如果是 OpenGL ICD *Mydriver.dll*，此项的值是**Mydriver.dll**。

<span id="OpenGLVersion"></span><span id="openglversion"></span><span id="OPENGLVERSION"></span>**OpenGLVersion**  
REG\_DWORD

OpenGL ICD OpenGL 运行时用来验证 OpenGL ICD 的版本的版本号。

<span id="OpenGLFlags"></span><span id="openglflags"></span><span id="OPENGLFLAGS"></span>**OpenGLFlags**  
REG\_DWORD

标志位掩码。 目前，位 0 (0x00000001) 设置的兼容性。 当设置位 1 (0x00000002) 时，OpenGL 运行时之前运行时调用 ICD 交换缓冲区函数不会调用 ICD 的 finish 函数。

32 位 Windows Vista 显示驱动程序在 64 位 Windows Vista 使用的是以下项：

<span id="UserModeDriverNameWow"></span><span id="usermodedrivernamewow"></span><span id="USERMODEDRIVERNAMEWOW"></span>**UserModeDriverNameWow**  
REG\_SZ

32 位 Microsoft Direct3D 用户模式的名称为 64 位 Windows Vista 显示驱动程序。

<span id="OpenGLDriverNameWow"></span><span id="opengldrivernamewow"></span><span id="OPENGLDRIVERNAMEWOW"></span>**OpenGLDriverNameWow**  
REG\_SZ

适用于 64 位 Windows Vista 的 32 位 OpenGL ICD 名称。

<span id="OpenGLVersionWow"></span><span id="openglversionwow"></span><span id="OPENGLVERSIONWOW"></span>**OpenGLVersionWow**  
REG\_DWORD

64 位 Windows Vista 32 位 OpenGL ICD 的版本号。

<span id="OpenGLFlagsWow"></span><span id="openglflagswow"></span><span id="OPENGLFLAGSWOW"></span>**OpenGLFlagsWow**  
REG\_DWORD

64 位 Windows Vista 32 位 OpenGL ICD 标志位掩码。

 

 





