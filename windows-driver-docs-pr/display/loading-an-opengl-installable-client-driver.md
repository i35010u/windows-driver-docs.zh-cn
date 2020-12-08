---
title: 加载 OpenGL 可安装客户端驱动程序
description: 加载 OpenGL 可安装客户端驱动程序
keywords:
- OpenGL ICD WDK 显示
- 正在加载驱动程序 WDK 显示
- ICD WDK 显示
- 可安装客户端驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec986fb097c430a6ddb1d41d3dff6d3675f91a1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796257"
---
# <a name="loading-an-opengl-installable-client-driver"></a>加载 OpenGL 可安装客户端驱动程序


OpenGL 运行时访问注册表，以确定要加载哪些 OpenGL 可安装客户端驱动程序 (ICD) 。 若要加载 OpenGL ICD，OpenGL 运行时：

-   确定与 OpenGL ICD 关联的名称、版本和标志，方法是调用 [**D3DKMTQueryAdapterInfo**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)函数，并将 KMTQAITYPE \_ UMOPENGLINFO 值设置为 *QUERYADAPTERINFO* 参数指向的 [**D3DKMT \_ pData**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)结构的 **类型** 成员。

-   检查 **D3DKMTQueryAdapterInfo** 返回的 opengl icd 的版本号，以验证 opengl icd 的版本。

-   使用 OpenGL ICD 的名称加载 OpenGL ICD。

-   初始化对 OpenGL ICD 函数的访问。
    **注意**   若要获取 OpenGL ICD 开发工具包的许可证，请联系 [Opengl 问题](mailto:opengl@microsoft.com) 团队。

     

若要查找 OpenGL ICD 的名称， [**D3DKMTQueryAdapterInfo**](/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo) 将在注册表中搜索以下项：

```registry
HKLM/System/CurrentControlSet/Control/Class/{Adapter GUID}/0000/
```

此密钥还包含 [Microsoft Direct3D 用户模式显示驱动程序](initializing-communication-with-the-direct3d-user-mode-display-driver.md)的名称。 此注册表项包含32位 windows vista 显示器驱动程序的四个注册表条目，用于32位 Windows Vista 上的四个条目，以及用于64位 Windows vista 的32位 Windows Vista 显示器驱动程序的四个条目。 以下条目适用于32位 windows Vista 显示器驱动程序，用于32位 Windows Vista：

<span id="UserModeDriverName"></span><span id="usermodedrivername"></span><span id="USERMODEDRIVERNAME"></span>**UserModeDriverName**  
REG\_SZ

Direct3D 用户模式显示驱动程序的名称，无论操作系统是否支持 OpenGL ICD，该驱动程序的操作都需要该驱动程序。

<span id="OpenGLDriverName"></span><span id="opengldrivername"></span><span id="OPENGLDRIVERNAME"></span>**OpenGLDriverName**  
REG\_SZ

OpenGL ICD 的名称。 例如，如果 *Mydriver.dll* OpenGL ICD，则 **Mydriver.dll** 此项的值。

<span id="OpenGLVersion"></span><span id="openglversion"></span><span id="OPENGLVERSION"></span>**OpenGLVersion**  
REG \_ DWORD

OpenGL 运行时用于验证 OpenGL ICD 版本的 OpenGL ICD 的版本号。

<span id="OpenGLFlags"></span><span id="openglflags"></span><span id="OPENGLFLAGS"></span>**OpenGLFlags**  
REG \_ DWORD

标志位掩码。 目前，位 0 (0x00000001) 设置为兼容。 如果设置了位 1 (0x00000002) ，则在运行时调用 ICD 的交换缓冲区函数之前，OpenGL 运行时不调用 ICD 的完成函数。

以下条目适用于32位 windows Vista 显示器驱动程序，用于64位 Windows Vista：

<span id="UserModeDriverNameWow"></span><span id="usermodedrivernamewow"></span><span id="USERMODEDRIVERNAMEWOW"></span>**UserModeDriverNameWow**  
REG\_SZ

64位 Windows Vista 的32位 Microsoft Direct3D 用户模式显示驱动程序的名称。

<span id="OpenGLDriverNameWow"></span><span id="opengldrivernamewow"></span><span id="OPENGLDRIVERNAMEWOW"></span>**OpenGLDriverNameWow**  
REG\_SZ

64位 Windows Vista 的32位 OpenGL ICD 的名称。

<span id="OpenGLVersionWow"></span><span id="openglversionwow"></span><span id="OPENGLVERSIONWOW"></span>**OpenGLVersionWow**  
REG \_ DWORD

64位 Windows Vista 的32位 OpenGL ICD 的版本号。

<span id="OpenGLFlagsWow"></span><span id="openglflagswow"></span><span id="OPENGLFLAGSWOW"></span>**OpenGLFlagsWow**  
REG \_ DWORD

64位 Windows Vista 的32位 OpenGL ICD 的标志位掩码。

 

