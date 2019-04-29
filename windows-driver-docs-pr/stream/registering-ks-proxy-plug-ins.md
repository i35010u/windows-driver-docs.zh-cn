---
title: 注册 KS 代理插件
description: 注册 KS 代理插件
ms.assetid: 1f8691cb-5371-4039-a081-7c422dcac5a8
keywords:
- 内核流式处理代理 WDK AVStream，注册插件
- 注册内核流式处理代理插件 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 199aa3085576dbf2242d7cd30bc503b0e7e4753d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358982"
---
# <a name="registering-ks-proxy-plug-ins"></a>注册 KS 代理插件


接口和属性页插件必须注册 KS 代理为 KS 代理扩展的提供程序。

若要注册插件，导出调用函数[DllRegisterServer](https://go.microsoft.com/fwlink/p/?linkid=106441)并[DllUnregisterServer](https://go.microsoft.com/fwlink/p/?linkid=106443)在实现 COM 对象的 DLL 中。 这些函数中声明*Olectl.h*但是用户定义的。

为组件的 CLSID、 该组件支持的接口的 IID，可以重复使用属性集的 GUID。

实现**DllRegisterServer**应执行以下操作：

1.  调用[AMovieDllRegisterServer2](https://go.microsoft.com/fwlink/p/?linkid=106448)值为**TRUE**注册筛选器。

2.  调用[RegCreateKeyEx](https://go.microsoft.com/fwlink/p/?linkid=106454)以创建端口和接收的句柄 HKLM\\系统\\CurrentControlSet\\控制\\MediaInterfaces 密钥。

3.  使用[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=106447)设置为 HKLM 下的值\\系统\\CurrentControlSet\\控制\\MediaInterfaces 键映射将属性设置为接口处理程序。 有关接口处理程序的详细信息，请参阅[界面处理程序插件](interface-handler-plug-in.md)。

4.  由于密钥不是预定义的注册表项之一，调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=106444)以关闭该密钥的句柄。

5.  调用**RegCreateKeyEx**。

6.  使用**RegSetValueEx**设置为 HKLM 下的值\\系统\\CurrentControlSet\\控制\\MediaSets\\映射属性的键设置为属性页。 有关属性页插件的详细信息，请参阅[属性页插件](property-page-plug-in.md)。

7.  由于密钥不是预定义的注册表项之一，调用**RegCloseKey**以关闭该密钥的句柄。

实现**DllUnregisterServer**应执行以下操作：

1.  调用**AMovieDllRegisterServer2**值为**FALSE**注销该筛选器。

2.  调用**RegCreateKeyEx**以打开现有的密钥。

3.  使用[RegDeleteKey](https://go.microsoft.com/fwlink/p/?linkid=106446)若要删除的子项。

4.  调用**RegCloseKey**以关闭该密钥的句柄。

 

 




