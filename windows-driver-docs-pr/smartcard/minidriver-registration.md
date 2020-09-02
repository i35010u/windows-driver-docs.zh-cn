---
title: 微型驱动程序注册
description: 微型驱动程序注册
ms.assetid: 332FEBD6-9803-4502-8F84-9DB2F17BB19B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e24c89803d0a809be4115905611317821cd5f16
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381449"
---
# <a name="minidriver-registration"></a>微型驱动程序注册


## <a name="span-iddllmainspanspan-iddllmainspanspan-iddllmainspandllmain"></a><span id="DllMain"></span><span id="dllmain"></span><span id="DLLMAIN"></span>DllMain


智能卡微型驱动程序实现并导出 [*DllMain*](/windows/desktop/Dlls/dllmain) 函数，以处理加载/卸载和附加/分离通知。 这允许微型驱动程序 DLL 管理其状态和已分配的资源。 有关实现的详细信息，请参阅 *DllMain* 参考主题。

## <a name="span-iddllregisterserver_and_dllunregisterserverspanspan-iddllregisterserver_and_dllunregisterserverspanspan-iddllregisterserver_and_dllunregisterserverspandllregisterserver-and-dllunregisterserver"></a><span id="DllRegisterServer_and_DllUnregisterServer"></span><span id="dllregisterserver_and_dllunregisterserver"></span><span id="DLLREGISTERSERVER_AND_DLLUNREGISTERSERVER"></span>DllRegisterServer 和 DllUnregisterServer


*DllRegisterServer* 和 *DllUnregisterServer* 不再被称为智能卡微型驱动程序规范的 v5 声明。 智能卡微型驱动程序是通过基于 INF 的系统注册表更新来执行的。

## <a name="span-id_registration_mechanismsspanspan-id_registration_mechanismsspanspan-id_registration_mechanismsspan-registration-mechanisms"></a><span id="_Registration_Mechanisms"></span><span id="_registration_mechanisms"></span><span id="_REGISTRATION_MECHANISMS"></span> 注册机制


应使用基于 INF 的方法来注册智能卡微型驱动程序。 INF 文件允许创建必要的注册表项以及从驱动程序包到适当目录的文件副本。

有关智能卡 INF 文件的示例，请参阅 [智能卡即插即用](smart-card-plug-and-play.md)。

## <a name="span-idinf_file_requirementsspanspan-idinf_file_requirementsspanspan-idinf_file_requirementsspaninf-file-requirements"></a><span id="INF_File_Requirements"></span><span id="inf_file_requirements"></span><span id="INF_FILE_REQUIREMENTS"></span>INF 文件要求


智能卡 INF 文件应包含为每个卡创建以下注册表项的指令。

``` syntax
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\VENDORCARDNAME]
"80000001"="VENDOR.dll"
"ATR"=hex:01,23,45,67,89,01,23,45,67,89,01,23,45,67,89,01,23,45
"ATRMask"=hex:ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff
```

如果微型驱动程序支持在 CAPI 下加载，则注册表文件中应包含以下行：

``` syntax
"Crypto Provider"="Microsoft Base Smart Card Crypto Provider"
```

如果微型驱动程序支持在 CNG 下加载，则注册表文件中应包含以下行：

``` syntax
"Smart Card Key Storage Provider"="Microsoft Smart Card Key Storage Provider"
```

 

