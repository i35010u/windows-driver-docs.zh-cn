---
title: 注册 KS 代理插件
description: 注册 KS 代理插件
ms.assetid: 1f8691cb-5371-4039-a081-7c422dcac5a8
keywords:
- 内核流式处理代理 WDK AVStream，注册插件
- 注册内核流式处理代理插件 WDK AVStream
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 25cedce82233a6c520dda1bf80d0986208f6ddb6
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073429"
---
# <a name="registering-ks-proxy-plug-ins"></a>注册 KS 代理插件

接口和属性页插件必须注册为 ks 代理扩展的提供程序。

若要注册插件，请在实现 COM 对象的 DLL 中导出称为[DllRegisterServer](https://docs.microsoft.com/windows/win32/api/olectl/nf-olectl-dllregisterserver)和[DllUnregisterServer](https://docs.microsoft.com/windows/win32/api/olectl/nf-olectl-dllunregisterserver)的函数。 这些函数在*Olectl*中声明，但是用户定义的。

您可以重复使用属性集的 GUID 作为组件的 CLSID 和该组件支持的接口的 IID。

**DllRegisterServer**的实现应执行以下操作：

1. 调用值为**TRUE**的[AMovieDllRegisterServer2](https://docs.microsoft.com/previous-versions//ms778973(v=vs.85))以注册筛选器。

1. 调用[RegCreateKeyEx](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regcreatekeyexa)创建并接收 HKLM \\ 系统 \\ CurrentControlSet \\ Control \\ MediaInterfaces 项的句柄。

1. 使用[RegSetValueEx](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regsetvalueexa)设置 HKLM \\ System CurrentControlSet Control MediaInterfaces 项下的一个值，用于将 \\ \\ \\ 属性集映射到接口处理程序。 有关接口处理程序的详细信息，请参阅[Interface Handler 插件](interface-handler-plug-in.md)。

1. 因为该密钥不是预定义的注册表项之一，所以调用[RegCloseKey](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regclosekey)关闭该密钥的句柄。

1. 调用**RegCreateKeyEx**。

1. 使用**RegSetValueEx**设置 HKLM \\ System CurrentControlSet Control MediaSets 项下的一个值，用于将 \\ \\ \\ \\ 属性集映射到属性页。 有关属性页插件的详细信息，请参阅[属性页插件](property-page-plug-in.md)。

1. 因为该密钥不是预定义的注册表项之一，所以调用**RegCloseKey**关闭该密钥的句柄。

**DllUnregisterServer**的实现应执行以下操作：

1. 调用**AMovieDllRegisterServer2** ，将值设置为**FALSE**以取消注册筛选器。

1. 调用**RegCreateKeyEx**打开现有密钥。

1. 使用[RegDeleteKey](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regdeletekeya)删除该子项。

1. 调用**RegCloseKey**关闭密钥的句柄。
