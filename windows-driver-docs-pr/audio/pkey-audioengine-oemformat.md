---
title: PKEY \_ AudioEngine \_ OEMFormat
description: PKEY \_ AudioEngine \_ OEMFormat
ms.assetid: a1587f46-1c21-4419-a1a4-81fe299c6871
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17312df4d3cf4945e287ea702b220275225d09df
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715008"
---
# <a name="pkey_audioengine_oemformat"></a>PKEY \_ AudioEngine \_ OEMFormat


在 Windows Vista 和更高版本中， **PKEY \_ AudioEngine \_ OEMFormat** 属性键用于标识音频终结点设备的默认流格式。 呈现和捕获设备都具有默认格式。 全局音频引擎使用设备的默认格式连接到设备以进行共享模式操作。 安装设备的 INF 文件会将设备的默认格式加载到注册表中。 用户可以通过 Windows 多媒体控制面板 ( # A0) 来更改默认格式。 Windows XP 和早期版本的 Windows 不支持 **PKEY \_ AudioEngine \_ OEMFormat** 属性键。

INF 文件在该设备的 "外接程序" 部分中指定音频终结点设备的默认格式。 以下 INF 示例显示了一个将终结点设备的默认格式加载到注册表中的 "添加注册表" 部分。

```inf
;;
;; Identify endpoint device as a set of speakers.
;; Set default format to 48-kHz, 16-bit stereo.
;; Add endpoint extension property page.
;;
[OEMSettingsOverride.AddReg]
HKR,"EP\\0", %PKEY_AudioEndpoint_Association%,,%KSNODETYPE_SPEAKER%
HKR,"EP\\0", %PKEY_AudioEngine_OEMFormat%, %REG_BINARY%, 41,00,00,00,28,00,00,00,
 FE,FF,02,00,80,BB,00,00,00,EE,02,00,04,00,10,00,16,00,10,00,03,00,00,00,01,00,
 00,00,00,00,10,00,80,00,00,AA,00,38,9B,71
HKR,"EP\\0", %PKEY_AudioEndpoint_ControlPanelProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID
```

前面的示例取自 Windows 驱动程序工具包中的 Sysfx 音频示例中的文件 Sysfx。 此 INF 文件的字符串部分包含以下定义。

```inf
PKEY_AudioEndpoint_ControlPanelProvider = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},1"
PKEY_AudioEndpoint_Association          = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMFormat              = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},3"
```

在前面的示例中，add-registry 部分的名称 OEMSettingsOverride AddReg，它是由 Sysfx 中接口安装部分的 [**AddReg**](../install/inf-addreg-directive.md) 指令定义的。 前面的示例将 ) 的字符串 "EP 0" (标识的终结点编号0的多个属性添加 \\ \\ 到设备接口的注册表项。  (如果设备接口表示具有多个终结点的 [波形筛选器](./wave-filters.md) ，则附加终结点的编号为1、2，依此类推 ) 。有关接口安装部分的详细信息，请参阅 [**INF AddInterface 指令**](../install/inf-addinterface-directive.md)。

在 INF 文件创建了三个属性键并将其关联值加载到注册表中后，应用程序可以通过获取终结点设备的 [IPropertyStore](/windows/win32/api/propsys/nn-propsys-ipropertystore) 接口访问这些属性。 Windows SDK 中的头文件 Mmdeviceapi 包含三个属性键的 C/c + + 定义。 有关获取 IPropertyStore 接口的详细信息，请参阅 Windows SDK 文档中的 [**IMMDevice：： OpenPropertyStore**](/windows/win32/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore) 方法说明。

在上述 INF 示例中， **PKEY \_ AudioEndpoint \_ Association** 属性键用于标识终结点设备的 KS pin 类别 GUID。 **PKEY \_ AudioEndpoint \_ ControlPanelProvider**属性键标识 COM 接口对象的类 GUID，该对象向终结点设备 Mmsys.cpl 中的属性页提供属性值。 有关这些属性键的详细信息，请参阅 Windows SDK 文档。 有关 KS pin 类别 Guid 的详细信息，请参阅 [固定类别属性](./pin-category-property.md)。

在前面的 INF 示例中，与 **PKEY \_ AudioEngine \_ OEMFormat** 属性键关联的属性值是一个48字节的注册表 \_ 二进制值，其中包含描述格式的 [**WAVEFORMATEX**](/windows/win32/api/mmreg/ns-mmreg-twaveformatex) 或 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构的序列化表示形式。 若要计算 \_ 要与**PKEY \_ AudioEngine \_ OEMFormat**属性键关联的 REG BINARY 数据值，请将**WAVEFORMATEX**或**WAVEFORMATEXTENSIBLE**结构嵌入到**PropVariant**结构中，然后通过调用**PropVariant**函数序列化**StgSerializePropVariant**结构。 有关 **PropVariant** 结构和 **StgSerializePropVariant** 函数的详细信息，请参阅 Windows SDK 文档。

下面的代码示例是一个控制台应用程序，它打印 \_ 前面的 INF 示例中显示的注册表项二进制数据。

```cpp
//
// Embed a WAVEFORMATEXTENSIBLE structure in a PropVariant
// container, and print the PropVariant structure as a
// serialized stream of bytes in REG_BINARY format.
//

#include <stdio.h>
#include <wtypes.h>
#include <propidl.h>
#include <propvarutil.h>
#include <mmreg.h>
#include <ks.h>
#include <ksmedia.h>

void PrintSerializedFormat(WAVEFORMATEX *pWfx)
{
    HRESULT hr;
    PROPVARIANT var;
    SERIALIZEDPROPERTYVALUE* pVal;
    ULONG cb;

    // Create a VT_BLOB from the WAVEFORMATEX structure.
    var.vt = VT_BLOB;
    var.blob.cbSize = sizeof(*pWfx) + pWfx->cbSize;
    var.blob.pBlobData = (BYTE*)pWfx;

    // Serialize the PROPVARIANT structure. The serialized byte stream
    // will eventually be written to the registry as REG_BINARY data.
    hr = StgSerializePropVariant(&var, &pVal, &cb);
    if (SUCCEEDED(hr))
    {
        // Write the binary data to stdout. Format the output so you can
        // copy and paste it directly into the INF file as REG_BINARY data.
        for (UINT i = 0; i < cb; i++)
        {
            BYTE b = ((BYTE*)pVal)[i];
            wprintf(L"%2.2X,", b);
        }

        wprintf(L"\n");
        CoTaskMemFree(pVal);
    }
}

//
// Use a WAVEFORMATEXTENSIBLE structure to specify the format
// for a 48-kHz, 16-bit, (2-channel) stereo audio stream.
//
void main()
{
    WAVEFORMATEXTENSIBLE wfx;

    wfx.Format.wFormatTag = WAVE_FORMAT_EXTENSIBLE;
    wfx.Format.nChannels = 2;
    wfx.Format.nSamplesPerSec = 48000;
    wfx.Format.nAvgBytesPerSec = 4*48000;
    wfx.Format.nBlockAlign = 4;
    wfx.Format.wBitsPerSample = 16;
    wfx.Format.cbSize = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
    wfx.Samples.wValidBitsPerSample = 16;
    wfx.dwChannelMask = 3;
    wfx.SubFormat = KSDATAFORMAT_SUBTYPE_PCM;

    PrintSerializedFormat(&wfx.Format);
}
```

前面的代码示例中的 main 函数创建一个 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构来说明默认格式。 您可以修改 main 函数以创建 [**WAVEFORMATEX**](/windows/win32/api/mmreg/ns-mmreg-twaveformatex) 或 **WAVEFORMATEXTENSIBLE** 结构来描述终结点设备的默认格式。

前面的代码示例中的 PrintSerializedFormat 函数序列化格式说明，并将序列化格式说明打印为 REG \_ 二进制数据。 可以复制该函数生成的打印输出，并将其粘贴到 INF 文件中。

 

