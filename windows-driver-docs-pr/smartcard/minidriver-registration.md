---
title: 微型驱动程序注册
description: 微型驱动程序注册
ms.assetid: 332FEBD6-9803-4502-8F84-9DB2F17BB19B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df83902740e4143861243de30ef4a11a91764c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545199"
---
# <a name="minidriver-registration"></a>微型驱动程序注册


## <a name="span-iddllmainspanspan-iddllmainspanspan-iddllmainspandllmain"></a><span id="DllMain"></span><span id="dllmain"></span><span id="DLLMAIN"></span>DllMain


智能卡微型驱动程序实现，并将导出[ *DllMain* ](https://msdn.microsoft.com/library/windows/desktop/ms682583)函数来处理加载/卸载并附加/分离通知。 这允许微型驱动程序 DLL 来管理其状态，并分配到的资源。 有关实现的详细信息，请参阅*DllMain*参考主题。

## <a name="span-iddllregisterserveranddllunregisterserverspanspan-iddllregisterserveranddllunregisterserverspanspan-iddllregisterserveranddllunregisterserverspandllregisterserver-and-dllunregisterserver"></a><span id="DllRegisterServer_and_DllUnregisterServer"></span><span id="dllregisterserver_and_dllunregisterserver"></span><span id="DLLREGISTERSERVER_AND_DLLUNREGISTERSERVER"></span>DllRegisterServer 和 DllUnregisterServer


*DllRegisterServer*并*DllUnregisterServer*与智能卡微型驱动程序规范 v5 指出不再调用。 通过对系统注册表的基于 INF 的更新执行卡微型驱动程序的注册。

## <a name="span-idregistrationmechanismsspanspan-idregistrationmechanismsspanspan-idregistrationmechanismsspan-registration-mechanisms"></a><span id="_Registration_Mechanisms"></span><span id="_registration_mechanisms"></span><span id="_REGISTRATION_MECHANISMS"></span> 注册机制


基于 INF 的方法应使用用于注册智能卡微型驱动程序。 INF 文件允许创建必要的注册表项，以及文件从驱动程序包复制到相应目录的副本

智能卡 INF 文件的示例，请参阅[智能卡即插](smart-card-plug-and-play.md)。

## <a name="span-idinffilerequirementsspanspan-idinffilerequirementsspanspan-idinffilerequirementsspaninf-file-requirements"></a><span id="INF_File_Requirements"></span><span id="inf_file_requirements"></span><span id="INF_FILE_REQUIREMENTS"></span>INF 文件要求


智能卡 INF 文件应包含创建的每个卡的以下注册表项的指令。

``` syntax
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\VENDORCARDNAME]
"80000001"="VENDOR.dll"
"ATR"=hex:01,23,45,67,89,01,23,45,67,89,01,23,45,67,89,01,23,45
"ATRMask"=hex:ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff
```

如果微型驱动程序支持加载下 CAPI，应在注册表文件中包含以下行：

``` syntax
"Crypto Provider"="Microsoft Base Smart Card Crypto Provider"
```

如果微型驱动程序支持在 CNG 下的加载，则应注册表文件中包括以下行：

``` syntax
"Smart Card Key Storage Provider"="Microsoft Smart Card Key Storage Provider"
```

 

 





