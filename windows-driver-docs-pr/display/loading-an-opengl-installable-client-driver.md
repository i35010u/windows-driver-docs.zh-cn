---
title: 加载 OpenGL 可安装客户端驱动程序
description: 加载 OpenGL 可安装客户端驱动程序
ms.assetid: 2b244bbf-f26c-4307-a347-a29e12c6d496
keywords:
- OpenGL ICD WDK 显示
- 正在加载驱动程序 WDK 显示
- ICD WDK 显示
- 可安装客户端驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a03d3197418eca3b5d71cfa09b655a3b7f17be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840603"
---
# <a name="loading-an-opengl-installable-client-driver"></a>加载 OpenGL 可安装客户端驱动程序


OpenGL 运行时访问注册表，以确定要加载的 OpenGL 可安装客户端驱动程序（ICD）。 若要加载 OpenGL ICD，OpenGL 运行时：

-   确定与 OpenGL ICD 关联的名称、版本和标志，方法是调用[**D3DKMTQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)函数，并在*QUERYADAPTERINFO*参数指向的[**D3DKMT\_pData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)结构的**类型**成员中设置 KMTQAITYPE\_UMOPENGLINFO 值。

-   检查**D3DKMTQueryAdapterInfo**返回的 opengl icd 的版本号，以验证 opengl icd 的版本。

-   使用 OpenGL ICD 的名称加载 OpenGL ICD。

-   初始化对 OpenGL ICD 函数的访问。
    **请注意**，   获取 Opengl ICD 开发工具包的许可证，请联系[opengl 问题](mailto:opengl@microsoft.com)团队。

     

若要查找 OpenGL ICD 的名称， [**D3DKMTQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)将在注册表中搜索以下项：

```registry
HKLM/System/CurrentControlSet/Control/Class/{Adapter GUID}/0000/
```

此密钥还包含[Microsoft Direct3D 用户模式显示驱动程序](initializing-communication-with-the-direct3d-user-mode-display-driver.md)的名称。 此注册表项包含32位 windows vista 显示器驱动程序的四个注册表条目，用于32位 Windows Vista 上的四个条目，以及用于64位 Windows vista 的32位 Windows Vista 显示器驱动程序的四个条目。 以下条目适用于32位 windows Vista 显示器驱动程序，用于32位 Windows Vista：

<span id="UserModeDriverName"></span><span id="usermodedrivername"></span><span id="USERMODEDRIVERNAME"></span>**UserModeDriverName**  
REG\_SZ

Direct3D 用户模式显示驱动程序的名称，无论操作系统是否支持 OpenGL ICD，该驱动程序的操作都需要该驱动程序。

<span id="OpenGLDriverName"></span><span id="opengldrivername"></span><span id="OPENGLDRIVERNAME"></span>**OpenGLDriverName**  
REG\_SZ

OpenGL ICD 的名称。 例如，如果 OpenGL ICD 为*Mydriver*，则此项的值为**Mydriver**。

<span id="OpenGLVersion"></span><span id="openglversion"></span><span id="OPENGLVERSION"></span>**OpenGLVersion**  
REG\_DWORD

OpenGL 运行时用于验证 OpenGL ICD 版本的 OpenGL ICD 的版本号。

<span id="OpenGLFlags"></span><span id="openglflags"></span><span id="OPENGLFLAGS"></span>**OpenGLFlags**  
REG\_DWORD

标志位掩码。 目前，位0（0x00000001）设置为兼容。 设置位1（0x00000002）后，在运行时调用 ICD 的交换缓冲区函数之前，OpenGL 运行时不调用 ICD 的完成函数。

以下条目适用于32位 windows Vista 显示器驱动程序，用于64位 Windows Vista：

<span id="UserModeDriverNameWow"></span><span id="usermodedrivernamewow"></span><span id="USERMODEDRIVERNAMEWOW"></span>**UserModeDriverNameWow**  
REG\_SZ

64位 Windows Vista 的32位 Microsoft Direct3D 用户模式显示驱动程序的名称。

<span id="OpenGLDriverNameWow"></span><span id="opengldrivernamewow"></span><span id="OPENGLDRIVERNAMEWOW"></span>**OpenGLDriverNameWow**  
REG\_SZ

64位 Windows Vista 的32位 OpenGL ICD 的名称。

<span id="OpenGLVersionWow"></span><span id="openglversionwow"></span><span id="OPENGLVERSIONWOW"></span>**OpenGLVersionWow**  
REG\_DWORD

64位 Windows Vista 的32位 OpenGL ICD 的版本号。

<span id="OpenGLFlagsWow"></span><span id="openglflagswow"></span><span id="OPENGLFLAGSWOW"></span>**OpenGLFlagsWow**  
REG\_DWORD

64位 Windows Vista 的32位 OpenGL ICD 的标志位掩码。

 

 





