---
title: 注册合成器
description: 注册合成器
keywords:
- DirectMusic 自定义呈现 WDK 音频，合成
- 用户模式下的自定义呈现 WDK 音频，合成
- 合成 WDK 音频，注册
- 注册合成
- 用户模式 synths WDK 音频，合成器注册
- 自定义 synths WDK 音频，合成器注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4778e41830e5cbeb17c34ca189593556cb433e13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800755"
---
# <a name="registering-your-synthesizer"></a>注册合成器


## <span id="registering_your_synthesizer"></span><span id="REGISTERING_YOUR_SYNTHESIZER"></span>


创建软件合成器后，必须将其添加到系统注册表中，以便应用程序可用作可枚举的 DirectMusic 端口。 当安装程序调用 DLL 的 [**DllRegisterServer**](/windows/win32/api/olectl/nf-olectl-dllregisterserver) COM 函数通知 dll 将自身注册为 COM 对象时，该函数也可注册合成器。 为此，该函数通过在以下路径中创建一个项来向可用软件合成程序列表添加条目：

```inf
  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\SoftwareSynths
```

标头文件 dmusicc. hdefines 常量 REGSTR \_ path \_ SOFTWARESYNTHS 表示此路径。

键的命名方式为合成器 COM 对象的类标识符。 键中的是一个名为 "Description" 的字符串字段，其名称为合成器的名称。

下面的示例代码演示了一个函数， `RegisterSynth` 可以从 **DllRegisterServer** 调用该函数以注册合成器：

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

`CLSIDToStr` 是一个本地定义的函数 (未显示在前面的代码示例中，) 该函数将 CLSID 值转换为字符串。 它类似于 Microsoft Windows SDK 文档中所述的 [**StringFromCLSID**](/windows/win32/api/combaseapi/nf-combaseapi-stringfromclsid) 函数。

 

