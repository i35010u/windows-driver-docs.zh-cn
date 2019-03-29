---
title: 注册合成器
description: 注册合成器
ms.assetid: c8cb30ba-97ca-49ee-a6ef-2938a0ab780e
keywords:
- DirectMusic 自定义呈现 WDK 音频，合成器
- 在用户模式 WDK 音频，合成器的自定义呈现
- 合成器 WDK 音频，注册
- 注册合成器
- 用户模式下 synths WDK 音频，合成器注册
- 自定义 synths WDK 音频，合成器注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd1f097de62f8db600962712e44d847e7ef14c61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564653"
---
# <a name="registering-your-synthesizer"></a>注册合成器


## <span id="registering_your_synthesizer"></span><span id="REGISTERING_YOUR_SYNTHESIZER"></span>


创建软件合成器后，它必须添加到系统注册表，这样就可用于应用程序作为可枚举的 DirectMusic 端口。 当安装程序调用 DLL 的[ **DllRegisterServer** ](https://msdn.microsoft.com/library/windows/desktop/ms682162) COM 函数以告知 DLL 以将自身注册为 COM 对象，该函数可以注册合成器也。 若要执行此操作，函数条目向列表中添加的可用软件合成器通过在以下路径中创建一个键：

```inf
  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\SoftwareSynths
```

标头文件 dmusicc.hdefines 常量 REGSTR\_路径\_SOFTWARESYNTHS 来表示此路径。

使用合成器 COM 对象的类标识符命名的密钥。 在密钥中的字符串字段称为"Description"具有名称合成器。

下面的代码示例显示了一个函数`RegisterSynth`，可以从调用**DllRegisterServer**注册合成器：

```cpp
  const char cszSynthRegRoot[] = REGSTR_PATH_SOFTWARESYNTHS "\\";
  const char cszDescriptionKey[] = "Description";
  const int CLSID_STRING_SIZE = 39;
  HRESULT CLSIDToStr(const CLSID &clsid, char *szStr, int cbStr);
 
  HRESULT RegisterSynth(REFGUID guid,
                        const char szDescription[])
  {
      HKEY hk;
      char szCLSID[CLSID_STRING_SIZE];
      char szRegKey[256];
 
      HRESULT hr = CLSIDToStr(guid, szCLSID, sizeof(szCLSID));
      if (!SUCCEEDED(hr))
      {
          return hr;
      }
 
      strcpy(szRegKey, cszSynthRegRoot);
      strcat(szRegKey, szCLSID);
 
      if (RegCreateKey(HKEY_LOCAL_MACHINE,
                       szRegKey,
                       &hk))
      {
          return E_FAIL;
      }
 
      hr = S_OK;
      if (RegSetValueEx(hk,
                        cszDescriptionKey,
                        0L,
                        REG_SZ,
                        (const unsigned char *)szDescription,
                        strlen(szDescription) + 1))
      {
          hr = E_FAIL;
      }
 
      RegCloseKey(hk);
      return hr;
  }
```

`CLSIDToStr` 是本地定义将 CLSID 值转换为字符字符串的函数 （不在前面的代码示例所示）。 它是类似于[ **StringFromCLSID** ](https://msdn.microsoft.com/library/windows/desktop/ms683917) Microsoft Windows SDK 文档中所述的函数。

 

 




